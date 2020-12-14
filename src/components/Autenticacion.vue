<template>
  <div class="container">
    <h1 class="text-center my-5">Inicia sesión</h1>
        <b-form @submit.prevent="login">
        <b-form-group
            id="input-group-1"
            label="Correo electrónico"
            label-for="input-1"
        >
            <b-form-input
            id="input-1"
            v-model="form.email"
            type="email"
            required
            placeholder="Escribe tu correo electrónico"
            ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Contraseña" label-for="input-2">
            <b-form-input
            id="input-2"
            v-model="form.password"
            type="password"
            required
            placeholder="Escribe tu contraseña"
            ></b-form-input>
        </b-form-group>

        <b-button type="submit" variant="primary">Iniciar sesión con Google</b-button>
        <b-button type="reset" variant="danger" class="ml-3">Reset</b-button>
        </b-form>
    </div>
</template>

<script>
import firebase from 'firebase';
export default {
    name: 'Autenticacion',
    data() {
      return {
        form: {
          email: '',
          password: '',
        },
        show: true
      }
    },
    methods: {
      login(){
          if (this.form.email && this.form.password && this.form.password.length >= 6){
              console.log("ingresa");              
              let provider = new firebase.auth.GoogleAuthProvider();
              firebase.auth().signInWithPopup(provider)
              .then(resp => {
                console.log(resp);
                this.$router.push('/listado');
                  this.error = '';
                }).catch(error => {
                console.error(error.code);
                console.error(error.message);
                if (error.code == "auth/wrong-password") {
                  this.errores(error);
                } else if(error.code == "auth/invalid-email") {
                  this.errores(error);
                } else if(error.code == "auth/user-disabled"){
                  this.errores(error);
                } else {
                  this.errores(error);
                  this.$router.push('/register');
                }
              })
          } else {
            console.log("No se puede conectar");
          }      
          }         
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
