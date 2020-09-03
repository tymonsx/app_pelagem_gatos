<template>
  <q-layout>
    <q-page>
      <div class="full-width text-center q-ma-sm">
        <img :src="img" alt="image" id="photo" class="photo" />
      </div>
      <div class="full-width text-center q-ma-sm">
        <q-file
          class="QFileGato"
          label="selecione uma foto de gato"
          outlined
          v-model="file"
          @input="carregaImagem"
          ><template v-slot:prepend> </template>
        </q-file>
      </div>
      <div id="divBotoes" class="full-width text-center">
        <q-btn id="botaoTirarFoto" color="primary" @click="takephoto()"
          >Tirar foto</q-btn
        ><br />
        <div id="msg" v-html="msg" class="textoPredito"></div>
        <div id="explicacaoPelagens">
          <tabbySpotted v-show="explicacaoTabbySpotted" />
          <tabbyMackerel v-show="explicacaoTabbyMackerel" />
          <tabbyClassic v-show="explicacaoTabbyClassic" />
          <solidColor v-show="explicacaoSolidColor" />
          <pointColor v-show="explicacaoPointColor" />
          <hairless v-show="explicacaoHairless" />
          <bicolor v-show="explicacaoBicolor" />
          <calico v-show="explicacaoCalico" />
          <tortoiseShell v-show="explicacaoTortoiseShell" />
        </div>
      </div>
      <q-list id="listaCompletaProbabilidades">
        <q-expansion-item
          label="Lista completa das probabilidades"
          group="listaProbabilidades"
          class="bg-secondary"
          style="text-align:left;"
        >
          <q-card>
            <div
              v-html="listaCompletaProbabiblidades"
              style="margin-left:5%;"
            ></div>
          </q-card>
        </q-expansion-item>
      </q-list>
    </q-page>
  </q-layout>
</template>
<style scoped>
.photo {
  height: 244px;
  width: 244px;
}

.textoPredito {
  white-space: pre-wrap;
  text-align: center;
  height: 30px;
}
.QFileGato {
  width: 200px;
  display: inline-block;
}
</style>

<script>
import * as tf from "@tensorflow/tfjs";
import { fetch as fetchPolyfill } from "whatwg-fetch";
import gatoExemplo from "assets/quasar-logo-full.svg";
import tabbySpotted from "components/TabbySpotted.vue";
import tabbyMackerel from "components/TabbyMackerel.vue";
import tabbyClassic from "components/TabbyClassic.vue";
import solidColor from "components/SolidColor.vue";
import pointColor from "components/PointColor.vue";
import hairless from "components/Hairless.vue";
import bicolor from "components/Bicolor.vue";
import calico from "components/Calico.vue";
import tortoiseShell from "components/TortoiseShell.vue";
export default {
  data() {
    return {
      height: 244,
      width: 244,
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
      valueToPredict: "",
      img: gatoExemplo,
      file: null,
      explicacaoTabbySpotted: false,
      explicacaoTabbyMackerel: false,
      explicacaoTabbyClassic: false,
      explicacaoSolidColor: false,
      explicacaoPointColor: false,
      explicacaoHairless: false,
      explicacaoBicolor: false,
      explicacaoCalico: false,
      explicacaoTortoiseShell: false,
      listaCompletaProbabiblidades: ""
    };
  },
  mounted() {
    // this.width = this.height * this.aspect;
    try {
      window.fetch = fetchPolyfill;
      this.carregar_modelo();

      this.explicacaoTabbySpotted = false;
      this.explicacaoTabbyMackerel = false;
      this.explicacaoTabbyClassic = false;
      this.explicacaoSolidColor = false;
      this.explicacaoPointColor = false;
      this.explicacaoHairless = false;
      this.explicacaoBicolor = false;
      this.explicacaoCalico = false;
      this.explicacaoTortoiseShell = false;
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
        .resizeBilinear(arrInput, [224, 224])
        .reshape([1, 224, 224, 3])
        .div(tf.scalar(255));
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
        "<b>" +
        this.labels[valor.argMax(-1).dataSync()[0]] +
        "</b>: " +
        (valor.dataSync()[valor.argMax(-1).dataSync()[0]] * 100).toFixed(4) +
        "%";

      switch (valor.argMax(-1).dataSync()[0]) {
        case 0:
          this.explicacaoBicolor = true;
          break;
        case 1:
          this.explicacaoCalico = true;
          break;
        case 2:
          this.explicacaoHairless = true;
          break;
        case 3:
          this.explicacaoPointColor = true;
          break;
        case 4:
          this.explicacaoSolidColor = true;
          break;
        case 5:
          this.explicacaoTabbyClassic = true;
          break;
        case 6:
          this.explicacaoTabbyMackerel = true;
          break;
        case 7:
          this.explicacaoTabbySpotted = true;
          break;
        case 8:
          this.explicacaoTortoiseShell = false;
          break;
      }
      this.listaCompletaProbabiblidades = "";
      valor.dataSync().forEach((element, index) => {
        let percent = (element * 100).toFixed(4);
        this.listaCompletaProbabiblidades +=
          " " + percent + "% - " + this.labels[index] + "<br>";
      });
    },
    carregaImagem() {
      this.predictedValue = "";
      this.img = URL.createObjectURL(this.file);

      console.log(this.file);
      this.msg = "Reconhecendo pelagem aguarde...";
      setTimeout(() => {
        this.predict();
      }, 2000);
    }
  },
  components: {
    tabbySpotted,
    tabbyMackerel,
    tabbyClassic,
    solidColor,
    pointColor,
    hairless,
    bicolor,
    calico,
    tortoiseShell
  }
};
</script>
