<template>
  <div>
    <Home titulo="MEVN" descripcion="2da prueba de MEVN"></Home>
    <Opciones nombre="Agregar"></Opciones>
    <Opciones nombre="Editar"></Opciones>
    <Opciones nombre="Eliminar"></Opciones>
    <Table></Table>
    <!-- <UploadImagen titulo="Subir archivos con Vue.js"></UploadImagen> -->
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Home from "./components/Home.vue";
import Table from "./components/Table.vue";
import Opciones from "./components/Opciones.vue";
import UploadImagen from "./components/UploadImagen.vue";

export default {
  name: "app",
  components: {
    // HelloWorld,
    Home,
    Table,
    Opciones,
    UploadImagen
  }
};
</script>

<style>
#app {
  background-color: red;
  color: #fff;
}
</style>
