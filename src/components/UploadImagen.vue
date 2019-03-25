<template>
  <div>
    <center>
      <h1>{{titulo}}</h1>
      <table>
        <tr>
          <td>Archivo</td>
          <td>
            <input type="file" accept="image/*" @change="uploadImage($event)" id="file-input">
          </td>
        </tr>
      </table>
    </center>
  </div>
</template>
<script>
import axios from "axios";
import { log } from "util";

export default {
  props: ["titulo"],
  name: "UploadImagen",
  data() {
    return {};
  },
  methods: {
    uploadImage(event) {
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
    }
  }
};
</script>