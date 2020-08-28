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
        ><br />

        <p id="msg" class="textoPredito">{{ msg }}</p>
      </div>
    </q-page>
  </q-layout>
</template>
<style scoped>
.photo {
  height: 250px;
  width: 250px;
}
.textoPredito {
  white-space: pre-wrap;
  text-align: center;
  height: 200px;
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
      labels: [
        "Bicolor",
        "Calico",
        "Hairless",
        "Point Color",
        "Solid Color",
        "Tabby Classic",
        "Tabby Mackerel",
        "Tabby Spotted",
        "Tortoiseshell"
      ],
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
          //this.msg = imgURI;
          //this.msg = "Reconhecendo Pelagem Aguarde...";

          document.getElementById("photo").src = imgURI;
          this.msg = "Reconhecendo pelagem aguarde...";
          setTimeout(() => {
            this.predict();
          }, 2000);
          //document.getElementById("photo").class = "photo";
          //this.processando = false;
        },
        msg => {
          //falha
          this.msg = msg;
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
      //this.msg = "Processando...";

      this.valueToPredict = document.getElementById("photo");
      let arrInput = tf.browser.fromPixels(this.valueToPredict); //
      this.valueToPredict = tf.image
        .resizeBilinear(arrInput, [150, 150])
        .reshape([1, 150, 150, 3]);
      let valor = "";
      try {
        valor = this.model.predict(this.valueToPredict);
      } catch (error) {
        alert(error);
      }

      //this.predictedValue = this.labels[valor.argMax(-1).dataSync()[0]];

      /*
      "Bicolor",
        "Calico",
        "Hairless",
        "Point Color",
        "Solid Color",
        "Tabby Classic",
        "Tabby Mackerel",
        "Tabby Spotted",
        "Tortoiseshell"
      */
      this.msg =
        valor.argMax(-1).dataSync()[0] +
        " - " +
        this.labels[valor.argMax(-1).dataSync()[0]] +
        ": " +
        (valor.dataSync()[valor.argMax(-1).dataSync()[0]] * 100).toFixed(4) +
        "%\n\n";

      valor.dataSync().forEach((element, index) => {
        this.msg +=
          " " +
          index +
          " - " +
          element.toFixed(4) +
          "% - " +
          this.labels[index] +
          "\n";
      });
    }
  }
};
</script>
