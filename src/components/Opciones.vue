<template>
  <div id="appOpciones"></div>
</template>
<script>
export default {
  props: ["nombre"],
  name: "Opciones",
  data() {
    return {};
  },
  methods: {
    imprimir() {
      if (this.nombre == "Agregar") {
        console.log("Opcion agregar");
      }
      if (this.nombre == "Editar") {
        console.log("Opcion Editar");
      }
      if (this.nombre == "Eliminar") {
        console.log("Opcion Eliminar");
      }
    }
  }
};
</script>
<style>
#appOpciones {
  text-align: center;
  margin-bottom: 10px;
}
</style>
