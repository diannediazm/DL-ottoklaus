<template>
    <div class="container my-5">
        <h2 class="mb-4">Editar producto</h2>
        <div v-if="this.$route.params.id">
            <b-form @submit.prevent="editarJuguetes">
                <b-form-group id="input-group-1" label="Código:" label-for="input-1">
                <b-form-input id="input-1" v-model="form.codigo" type="text" required placeholder="Ingresar Código"></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-1" label="Nombre:" label-for="input-1">
                <b-form-input id="input-1" v-model="form.nombre" type="text" required placeholder="Ingresar Nombre"></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-2" label="Stock:" label-for="input-2">
                <b-form-input id="input-2" v-model="form.stock" type="number" required placeholder="Ingresar Stock"></b-form-input>
            </b-form-group>

            <b-form-group id="input-group-3" label="Precio:" label-for="input-3">
                <b-form-input id="input-3" v-model="form.precio" type="number" required placeholder="Ingresar Precio"></b-form-input>
            </b-form-group>

                <b-button type="submit" variant="primary" class="mx-1">Editar</b-button>
                <b-button type="reset" variant="danger" class="mx-1">Reset</b-button>
                <b-button type="reset" variant="info" class="mx-1" @click="$router.push('/listado')">Volver</b-button>
            </b-form>
        </div>
    </div>
</template>

<script>
export default {
    name: 'EditarProducto',
    data() {
        return {
            form: {
                    codigo: '',
                    nombre: '',
                    stock: '',
                    precio: '',
                }
        }
    },
    created() {
        let datos = {};
        datos = this.$store.getters.mostrarJuguetes.find(resp => resp.id === this.$route.params.id)
        if (datos){
            this.form.codigo = datos.codigo;
            this.form.nombre = datos.nombre;
            this.form.stock = datos.stock;
            this.form.precio = datos.precio;
            this.form.id = datos.id;
        }else {
            this.$message('Este juguete no existe');
            setTimeout(()=>{
                this.$router.push('/listado');
            },1000);
        }
    },
    methods: {
        editarJuguetes(){
            if (this.form.codigo && this.form.nombre && this.form.nombre.length > 2 && this.form.stock && this.form.stock > 0 && this.form.precio && this.form.precio > 0){
                let data = {
                    codigo: this.form.codigo,
                    nombre: this.form.nombre,
                    stock: parseInt(this.form.stock),
                    precio: parseInt(this.form.precio),
                    id: this.form.id,
                }
                this.$confirm('¿Quieres editar este producto?', 'Informativo', {
                            confirmButtonText: 'Sí',
                            cancelButtonText: 'No',
                            type: 'info',
                            center: true
                            }).then(() => {
                            this.$message({
                                type: 'success',
                                message: 'Producto editado'
                            });
                            this.$store.dispatch('editarJuguetes', data);
                            }).catch(() => {
                            this.$message({
                                type: 'info',
                                message: 'Acción cancelada'
                            });          
                        });               
            } else {
                console.log("No se puede");
            }
        }
    },
}
</script>