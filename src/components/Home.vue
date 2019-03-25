<template>
  <div id="appHome">
    <center>
      <h1>{{titulo}}</h1>
      <p>{{descripcion}}</p>
    </center>
  </div>
</template>
<script>
export default {
  props: ["titulo", "descripcion"],
  name: "Home",
  data() {
    return {};
  },
  methods: {}
};
</script>