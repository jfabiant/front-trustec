<template>
  <div id="appTable">
    <center>
      <form class="form-inline" autocomplete="nope">
        <table border="1px solid #000">
          <tr>
            <td>Nombre</td>
            <td>
              <input
                v-model="datos.nombre"
                type="text"
                class="form-control ml-sm-2 mr-sm-4 my-2"
                required
              >
            </td>
          </tr>
          <tr>
            <td>Descripcion</td>
            <td>
              <input
                v-model="datos.descripcion"
                type="text"
                class="form-control ml-sm-2 mr-sm-4 my-2"
                required
              >
            </td>
          </tr>
          <tr>
            <td>Imagen</td>
            <td>
              <input type="file" accept="image/*" @change="onSubmit($event)" id="file-input">
            </td>
          </tr>
          <tr>
            <!-- <button type="submit" class="btn btn-primary my-2" id="btnAgregar">Agregar</button> -->
          </tr>
        </table>
      </form>
      <br>
      <table border="1px solid #000">
        <tr>
          <td>Id</td>
          <td>Nombre</td>
          <td>Descripcion</td>
          <td>Imagen</td>
          <td colspan="2">Opciones</td>
        </tr>
        <tr v-for="product in sortedProducts" v-bind:key="product.id">
          <td>{{product.idproducto}}</td>
          <td>{{product.nombre}}</td>
          <td>{{product.descripcion}}</td>
          <td>
            <!-- Con esto conseguimos que -->
            <img
              v-bind:src="'http://localhost:3000/api/containers/container1/download/' + product.imagen + ''"
              v-bind:alt="product.imagen"
              v-bind:width="100"
            >
          </td>
          <td>
            <button class="icon-button" v-on:click="onDelete(product.idproducto)">Eliminar</button>
          </td>
        </tr>
      </table>
    </center>
  </div>
</template>
<script>
import axios from "axios";

let defaultData = {
  nombre: null,
  descripcion: null,
  imagen: null
};

export default {
  props: [""],
  name: "Table",
  data() {
    return {
      products: [],
      datos: defaultData,
      files: []
    };
  },
  created() {
    this.getProducts();
  },
  computed: {
    sortedProducts() {
      return this.products.slice().sort((a, b) => {
        return a.product_id - b.product_id;
      });
    }
  },
  methods: {
    addFiles() {
      this.$refs.files.click();
    },

    async getProducts() {
      const products = [];
      const resGetProducts = await axios({
        url: "http://localhost:3000/api/productos/productos",
        method: "GET"
      });
      for (let i = 0; i < resGetProducts.data.length; i++) {
        products.push(resGetProducts.data[i]);
        // console.log(products[i]);
      }
      this.products = products;
    },
    async onSubmit(event) {
      let date = new Date();
      // Get date now
      let hora = date.getHours();
      let minute = date.getMinutes();
      let second = date.getSeconds();

      let dateNow = `${hora}${minute}${second}`;

      const resPostProducts = await axios({
        url: "http://localhost:3000/api/productos/productos",
        method: "POST",
        data: {
          nombre: defaultData.nombre,
          descripcion: defaultData.descripcion,
          imagen: event.target.files[0].name
        }
      });

      defaultData.nombre = "";
      defaultData.descripcion = "";

      console.log("Method: Upload Image");

      const URL = "http://localhost:3000/api/containers/container1/upload";

      let data = new FormData();

      data.append("name", "my-picture");
      data.append("file", event.target.files[0]);

      console.log(" ########## DATA ########## ");

      // Bingo
      console.log(event.target.files[0].name);

      let config = {
        header: {
          "Content-Type": "image/png"
        }
      };

      axios.post(URL, data, config).then(response => {
        console.log("###### RESPONSE ######");
        console.log(response);
      });

      await this.getProducts();
    },
    async onDelete(id) {
      const resDeleteProducts = await axios({
        url: "http://localhost:3000/api/productos/productos",
        method: "DELETE",
        data: {
          id: id
        }
      });
      await this.getProducts();
    }
  }
};
</script>
<style>
.icon-button {
  background: red;
  padding: 10px;
  color: #fff;
}
</style>

