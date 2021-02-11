<template>
  <q-page class="flex flex-center">
    <div class="full-width text-center" style="margin-top: 1%;">
      <img :src="img" alt="Imagem selecionada" id="foto" class="photo" />
    </div>
    <div class="text-center">
      <q-file
        class="QFileGato"
        label="Selecione uma foto de gato"
        outlined
        v-model="arquivo"
        @input="carregarImagem"
        ><template v-slot:prepend> </template>
      </q-file>
    </div>
    <div id="divBotoes" class="full-width text-center q-gutter-sm">
      <q-btn id="btnTirarFoto" color="primary" @click="tirarFoto()"
        >Tirar foto</q-btn
      >
    </div>
    <div id="msg" v-html="msgPredicao" class="textoPredito"></div>
    <div id="explicacaoPelagens" class="full-width text-center">
      <tabbySpotted
        class="full-width text-center"
        v-show="explicacaoTabbySpotted"
      />
      <tabbyMackerel
        class="full-width text-center"
        v-show="explicacaoTabbyMackerel"
      />
      <tabbyClassic
        class="full-width text-center"
        v-show="explicacaoTabbyClassic"
      />
      <solidColor
        class="full-width text-center"
        v-show="explicacaoSolidColor"
      />
      <pointColor
        class="full-width text-center"
        v-show="explicacaoPointColor"
      />
      <hairless class="full-width text-center" v-show="explicacaoHairless" />
      <bicolor class="full-width text-center" v-show="explicacaoBicolor" />
      <calico class="full-width text-center" v-show="explicacaoCalico" />
      <tortoiseShell
        class="full-width text-center"
        v-show="explicacaoTortoiseShell"
      />
    </div>
    <q-list id="listaCompletaProbabilidades" class="full-width text-center">
      <q-expansion-item
        label="Lista completa das probabilidades"
        group="listaProbabilidades"
        class="bg-secondary"
        style="text-align:left;"
      >
        <q-card>
          <div
            v-html="listaCompletaProbabiblidades"
            class="text-justify"
            style="text-align: left; margin-left:2%;"
          ></div>
        </q-card>
      </q-expansion-item>
    </q-list>
  </q-page>
</template>
<style scoped>
.photo {
  height: 224px;
  width: 224px;
}
.QFileGato {
  width: 224px;
  display: inline-block;
}
.textoPredito {
  white-space: pre-wrap;
  text-align: center;
  height: 3%;
  margin-top: 2%;
}
</style>

<script>
import * as tf from "@tensorflow/tfjs";
import { fetch as fetchPolyfill } from "whatwg-fetch";
import gatoExemplo from "assets/logo.png";
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
      msgPredicao: "Tire uma foto do gato",
      modelo: tf.sequential(),
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
      objetoPredicao: "",
      img: gatoExemplo,
      arquivo: null,
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
    try {
      window.fetch = fetchPolyfill;
      this.limparExplicacao();
      this.carregarModelo();
    } catch (error) {
      alert(error);
    }
  },
  methods: {
    async carregarModelo() {
      this.msgPredicao = "Carregando Modelo ...";
      try {
        this.modelo = await tf.loadLayersModel("model/model.json");
      } catch (error) {
        alert(error);
      }
      this.msgPredicao = "Modelo Carregado";
    },
    limparExplicacao() {
      this.explicacaoTabbySpotted = false;
      this.explicacaoTabbyMackerel = false;
      this.explicacaoTabbyClassic = false;
      this.explicacaoSolidColor = false;
      this.explicacaoPointColor = false;
      this.explicacaoHairless = false;
      this.explicacaoBicolor = false;
      this.explicacaoCalico = false;
      this.explicacaoTortoiseShell = false;
    },
    tirarFoto() {
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
          document.getElementById("foto").src = imgURI;
          this.limparExplicacao();
          this.msgPredicao = "Reconhecendo pelagem aguarde...";
          setTimeout(() => {
            this.predizerImagem();
          }, 2000);
        },
        msg => {
          this.msgPredicao = msg;
        },
        opts
      );
    },
    predizerImagem() {
      this.objetoPredicao = document.getElementById("foto");

      let arrInput = tf.browser.fromPixels(this.objetoPredicao);
      this.objetoPredicao = tf.image
        .resizeBilinear(arrInput, [224, 224])
        .reshape([1, 224, 224, 3])
        .div(tf.scalar(255));
      let valor = "";
      try {
        valor = this.modelo.predict(this.objetoPredicao);
      } catch (error) {
        alert(error);
      }

      this.msgPredicao =
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
          this.explicacaoTortoiseShell = true;
          break;
      }

      this.listaCompletaProbabiblidades = "";
      valor.dataSync().forEach((element, index) => {
        let percent = (element * 100).toFixed(4);
        this.listaCompletaProbabiblidades +=
          " " + percent + "% - " + this.labels[index] + "<br>";
      });
    },
    carregarImagem() {
      this.img = URL.createObjectURL(this.arquivo);

      this.msgPredicao = "Reconhecendo pelagem aguarde...";
      this.limparExplicacao();
      setTimeout(() => {
        this.predizerImagem();
      }, 500);
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
