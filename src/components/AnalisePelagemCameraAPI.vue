<template>
  <q-layout>
    <q-page class="">
      <div class="full-width text-center q-ma-sm">
        <img
          src="~assets/quasar-logo-full.svg"
          alt="image"
          id="photo"
          class="photo"
        />
      </div>

      <div id="divBotoes" class="full-width text-center">
        <q-btn id="botaoTirarFoto" color="primary" @click="takephoto()"
          >Tirar foto</q-btn
        >

        <p id="msg">{{ msg }}</p>
      </div>
    </q-page>
  </q-layout>
</template>
<style scoped>
.photo {
  height: 250px;
  width: 250px;
}
</style>

<script>
import * as tf from "@tensorflow/tfjs";
import { fetch as fetchPolyfill } from "whatwg-fetch";

export default {
  data() {
    return {
      height: 250,
      width: 250,
      aspect: 16 / 9,
      msg: "Tire uma foto do gato",
      model: tf.sequential(),
      labels: ["solid", "mackerel"],
      valueToPredict: ""
    };
  },
  mounted() {
    // this.width = this.height * this.aspect;
    try {
      window.fetch = fetchPolyfill;
      this.carregar_modelo();
    } catch (error) {
      alert(error);
    }
  },
  methods: {
    takephoto() {
      let opts = {
        quality: 100,
        destinationType: Camera.DestinationType.FILE_URI,
        sourceType: Camera.PictureSourceType.CAMERA,
        mediaType: Camera.MediaType.PICTURE,
        encodingType: Camera.EncodingType.JPEG,
        cameraDirection: Camera.Direction.BACK,
        correctOrientation: true,
        targetWidth: this.width,
        targetHeight: this.height
      };

      navigator.camera.getPicture(
        imgURI => {
          //sucesso
          document.getElementById("msg").textContent = imgURI;
          document.getElementById("photo").src = imgURI;
          this.predict();
          //document.getElementById("photo").class = "photo";
        },
        msg => {
          //falha
          document.getElementById("msg").textContent = msg;
        },
        opts
      );
    },
    async carregar_modelo() {
      this.msg = "Carregando Modelo ...";
      try {
        this.model = await tf.loadLayersModel("model/model.json");
      } catch (error) {
        alert(error);
      }
      this.msg = "Modelo Carregado";
    },
    predict() {
      this.msg = "Processando...";
      this.valueToPredict = document.getElementById("photo");
      let arrInput = tf.browser.fromPixels(this.valueToPredict); //
      this.valueToPredict = tf.image
        .resizeBilinear(arrInput, [224, 224])
        .reshape([1, 224, 224, 3]);
      let valor = "";
      try {
        valor = this.model.predict(this.valueToPredict);
      } catch (error) {
        alert(error);
      }

      //this.predictedValue = this.labels[valor.argMax(-1).dataSync()[0]];
      // let pcentCovid = (valor.dataSync()[0] * 100).toFixed(4);
      //let pcentNormal = (valor.dataSync()[1] * 100).toFixed(4);
      this.msg =
        this.labels[valor.argMax(-1).dataSync()[0]] +
        ": " +
        (valor.argMax(-1).dataSync()[0] * 100).toFixed(4) +
        "%";
    }
  }
};
</script>
