<template>
    <div class="container text-center my-5">
        <h1>Listado de juguetes</h1>
        <b-button variant="info" class="my-5" data-toggle="modal" data-target="#exampleModal">Agregar producto</b-button>
        <el-table
          :data="dataJuguetes"
          style="width: 100%">
            <el-table-column
              label="Código"
              width="200">
              <template slot-scope="scope">
                <span style="margin-left: 10px">{{ scope.row.codigo }}</span>
              </template>
            </el-table-column>
            <el-table-column
              label="Nombre"
              width="250">
              <template slot-scope="scope">
                  <div slot="reference" class="name-wrapper">
                    <el-tag size="medium">{{ scope.row.nombre }}</el-tag>
                  </div>
              </template>
            </el-table-column>
            <el-table-column
              label="Stock"
              width="200">
              <template slot-scope="scope">
                  <div slot="reference" class="name-wrapper">
                    <el-tag size="medium">{{ scope.row.stock }}</el-tag>
                  </div>
              </template>
            </el-table-column>
            <el-table-column
              label="Precio"
              width="150">
              <template slot-scope="scope">
                  <div slot="reference" class="name-wrapper">
                    <el-tag size="medium">{{ scope.row.precio }}</el-tag>
                  </div>
              </template>
            </el-table-column>
            <el-table-column
              label="Operaciones"
              width="250">
              <template slot-scope="scope">
                <el-button
                  size="mini"
                  type="success"
                  class="mr-5"
                  @click="handleEdit(scope.row.id)">Editar</el-button>
                <el-button
                  size="mini"
                  type="danger"
                  @click="handleDelete(scope.row.id)">Eliminar</el-button>
              </template>
            </el-table-column>
        </el-table>
   </div>
</template>

<script>
export default {
    name: 'ListadoJuguetes',
    computed: {
        dataJuguetes() {
            return this.$store.getters.mostrarJuguetes;
        }
    },
    methods: {
      handleDelete(id){
        this.$confirm('¿Seguro que desea eliminar este producto?', 'Advertencia', {
          confirmButtonText: 'Sí',
          cancelButtonText: 'No',
          type: 'warning',
          center: true
        }).then(() => {
          this.$message({
            type: 'success',
            message: 'Eliminado'
          });
          this.$store.dispatch('eliminarJuguetes',id);
        }).catch(() => {
          this.$message({
            type: 'info',
            message: 'No se ha eliminado'
          });          
        });
      },
      handleEdit(id){
        this.$router.push({name: 'Editar', params:{id:id}});
      }
    },
}
</script>