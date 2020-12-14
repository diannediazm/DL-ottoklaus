<template>
    <div>
        <b-navbar toggleable type="dark" variant="dark">
            <b-navbar-brand href="/">OTTO KLAUS</b-navbar-brand>
            <div class="links">
            <b-nav-item href="" @click="login">Login</b-nav-item>
            <b-nav-item href="" @click="salida">Logout</b-nav-item>
            </div>
        </b-navbar>
        <router-view/>
    </div>
</template>

<script>
import firebase from 'firebase';
export default {
    name: 'Navbar',
    methods: {
      login(){            
        let provider = new firebase.auth.GoogleAuthProvider();
        firebase.auth().signInWithPopup(provider)
        .then(resp => {
          console.log(resp);
          this.$router.push('/listado');
          this.error = '';
            }).catch((error)=>{
                this.error = '';
                console.error(error);
                if (error.code == 'auth/user-not-found'){
                alert("El usuario no existe en nuestra base de datos");
                }else if(error.code == 'auth/wrong-password'){
                alert("La contraseña no es válida o el usuario no tiene una contraseña.");
                }else {
                alert(error.message);
                }
              })
      },  
      salida(){
      firebase.auth().signOut().then(()=>{
        console.log("salida de usuario")
        this.$router.replace('/');
      })
      }
    }    
}

</script>

<style lang="scss">
.links {
  list-style: none;
  display: flex;
  margin-left: 1000px;
  }
.nav-link {
  color: white;
}
    
</style>