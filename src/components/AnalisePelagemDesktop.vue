<template>
  <q-page class="flex flex-center">
    <div class="full-width text-center">
      <img
        :src="img"
        alt="image"
        id="foto"
        class="photo"
        style="object-fit:cover;"
        v-show="displayFoto"
      />
      <video
        id="video"
        class="desktop-only text-center photo"
        style="object-fit:cover;"
        v-show="displayVideo"
      >
        Video não disponível.
      </video>
      <canvas
        id="canvas"
        style="object-fit:cover;"
        class="photo"
        v-show="displayCanvas"
      />
    </div>
    <div class="text-center">
      <q-file
        class="QFileGato"
        label="selecione uma foto de gato"
        outlined
        v-model="arquivo"
        @input="carregarImagem"
        v-show="displayQFile"
        ><template v-slot:prepend> </template>
      </q-file>
    </div>
    <div id="divBotoes" class="full-width text-center q-gutter-sm">
      <q-btn
        id="btnTirarFoto"
        color="primary"
        @click="tirarFoto()"
        v-show="btnTirarFoto"
        >Tirar foto</q-btn
      >
      <q-btn
        id="btnAtivarVideo"
        color="primary"
        class="desktop-only"
        @click="ativarVideo()"
        v-show="btnAtivarVideo"
        >Ativar Vídeo</q-btn
      >
      <q-btn
        id="btnEncerrarVideo"
        color="primary"
        class="desktop-only"
        v-show="btnEncerrarVideo"
        @click="encerrarVideo()"
        >Encerrar Vídeo</q-btn
      >
    </div>
    <div id="msg" v-html="msgPredicao" class="full-width textoPredito"></div>
    <div
      id="explicacaoPelagens"
      class="full-width"
      v-show="divExplicacaoPelagens"
    >
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
    <q-list id="listaCompletaProbabilidades">
      <q-expansion-item
        label="Lista completa das probabilidades"
        group="listaProbabilidades"
        class="full-width bg-secondary"
      >
        <q-card>
          <div v-html="listaCompletaProbabiblidades" class="full-width"></div>
        </q-card>
      </q-expansion-item>
    </q-list>
  </q-page>
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
  width: 244px;
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
      msgPredicao: "Modelo carregado",
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
      listaCompletaProbabiblidades: "",
      canvas: "",
      stream: null,
      displayFoto: true,
      displayVideo: false,
      displayCanvas: false,
      displayCapturaTela: false,
      btnAtivarVideo: true,
      btnEncerrarVideo: false,
      btnTirarFoto: false,
      divExplicacaoPelagens: false,
      displayQFile: true
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

    this.canvas = document.getElementById("canvas");
    this.canvas.width = video.width = this.width;
    this.canvas.height = video.width = this.height;
  },
  methods: {
    async carregarModelo() {
      this.msgPredicao = "Carregando modelo ...";
      try {
        this.modelo = await tf.loadLayersModel("model/model.json");
      } catch (error) {
        alert(error);
      }
      this.msgPredicao = "Modelo carregado";
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
      this.divExplicacaoPelagens = false;
      this.listaCompletaProbabiblidades = "";
    },
    ativarVideo() {
      this.displayFoto = false;
      this.displayVideo = true;
      this.displayCanvas = false;
      this.btnAtivarVideo = false;
      this.btnTirarFoto = true;
      this.btnEncerrarVideo = true;
      this.limparExplicacao();
      this.msgPredicao = "Clique em tirar foto";
      this.displayQFile = false;

      this.stream = navigator.mediaDevices
        .getUserMedia({
          audio: false,
          video: true
        })
        .then(function(stream) {
          video.srcObject = stream;
          video.play();
          return stream;
        })
        .then(stream => {
          this.stream = stream;
        })
        .catch(function(err) {
          console.log("An error occurred: " + err);
        });
    },
    tirarFoto() {
      var context = canvas.getContext("2d");
      context.drawImage(video, 0, 0, canvas.width, canvas.height);
      var data = canvas.toDataURL("image/png");
      this.img = data;
      this.displayFoto = true;
      this.displayVideo = false;
      this.displayCanvas = false;
      this.btnAtivarVideo = false;
      this.btnTirarFoto = false;
      this.btnEncerrarVideo = true;
      this.divExplicacaoPelagens = true;
      this.predizerImagem();
    },
    encerrarVideo() {
      this.displayVideo = false;
      this.displayCanvas = false;
      this.displayFoto = true;
      this.btnAtivarVideo = true;
      this.btnTirarFoto = false;
      this.btnEncerrarVideo = false;
      this.img = gatoExemplo;
      this.msgPredicao = "Modelo carregado";
      this.displayQFile = true;
      this.arquivo = null;
      this.limparExplicacao();

      document.getElementById("video").srcObject = null;

      this.stream.getTracks().forEach(function(track) {
        if (track.kind == "video") {
          track.stop();
          track.enabled = false;
        }
      });
    },
    predizerImagem() {
      this.divExplicacaoPelagens = true;
      this.msgPredicao = "Reconhecendo pelagem aguarde...";
      this.objetoPredicao = document.getElementById("foto");
      let arrInput = tf.browser.fromPixels(this.objetoPredicao); //
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
      this.displayFoto = true;
      this.displayVideo = false;
      this.displayCanvas = false;

      this.objetoPredicao = "";
      this.img = URL.createObjectURL(this.arquivo);

      this.msgPredicao = "Reconhecendo pelagem aguarde...";

      this.limparExplicacao();
      this.predizerImagem();
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
