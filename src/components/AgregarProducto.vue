<template>
    <div class="container my-5">
        <h2 class="text-center mb-4">Agregar Producto</h2>
        <b-form @submit.prevent="agregar">
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

            <b-button type="submit" variant="primary">Agregar</b-button>
            <b-button type="reset" variant="danger" class="mx-3">Reset</b-button>
        </b-form>
    </div>
</template>

<script>
    export default {
        name: 'AgregarProducto',
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
        methods: {
            agregar(){
                if (this.form.codigo && this.form.nombre && this.form.nombre.length > 2 && this.form.stock && this.form.stock > 0 && this.form.precio && this.form.precio > 0) {
                        this.$confirm('¿Quieres agregar un producto?', 'Informativo', {
                            confirmButtonText: 'Sí',
                            cancelButtonText: 'No',
                            type: 'info',
                            center: true
                            }).then(() => {
                            this.$message({
                                type: 'success',
                                message: '¡El producto se creó!'
                            });
                            this.$store.dispatch('agregarJuguete', this.form);
                            this.$router.push('/listado');
                            }).catch(() => {
                            this.$message({
                                type: 'info',
                                message: 'El producto no se creó'
                            });          
                        });               
                } else {
                    console.log("No funciona");
                }
            }
        },
    }
</script>