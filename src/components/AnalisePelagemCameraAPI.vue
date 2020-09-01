<template>
  <q-layout>
    <q-page class="">
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
        <div
          id="explicacaoPelagem"
          v-html="explicacaoPelagem"
          style="text-align:center;"
        ></div>
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
  height: 30px;
}
.QFileGato {
  width: 250px;
  display: inline-block;
}
</style>

<script>
import * as tf from "@tensorflow/tfjs";
import { fetch as fetchPolyfill } from "whatwg-fetch";
import gatoExemplo from "assets/quasar-logo-full.svg";
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
      valueToPredict: "",
      img: gatoExemplo,
      file: null,
      explicacaoPelagem: "",
      listaCompletaProbabiblidades: ""
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
        "<b>" +
        this.labels[valor.argMax(-1).dataSync()[0]] +
        "</b>: " +
        (valor.dataSync()[valor.argMax(-1).dataSync()[0]] * 100).toFixed(4) +
        "%";

      switch (valor.argMax(-1).dataSync()[0]) {
        case 0:
          this.explicacaoPelagem =
            "Bicolor: geralmente possuem uma cor predominamente branca. A cor secundária pode estar presente em formato de manchas aleatórias ('magpie'), manchas aleatórias com cauda colorida ('harlequin') ou manchas coloridas na cabeça e nas costas (van).";
          break;
        case 1:
          this.explicacaoPelagem =
            "Calico: com bastantes semelhanças ao tortoise shell, sua principal diferença é a presença da tonalidade branca.";
          break;
        case 2:
          this.explicacaoPelagem =
            "Hairless: possuem este nome pela quase completa ausência de pelagem.";
          break;
        case 3:
          this.explicacaoPelagem =
            "Point color: possuem coloração diferente da cor primária somente na cabeça, patas e cauda.";
          break;
        case 4:
          this.explicacaoPelagem =
            "Solid color: possuem somente uma cor por toda a sua extensão.";
          break;
        case 5:
          this.explicacaoPelagem =
            "Tabby classic: possuem listras largas na cor preta e geralmente sua cor predominamente é mais clara. Há também a presença de uma espécie de 'redemoinho' em sua pelagem.";
          break;
        case 6:
          this.explicacaoPelagem =
            "Tabby mackerel: possuem listras verticais e mais finas que as do 'tabby classic'. Sua principal característica é um desenho em formato de 'M' no meio de sua testa.";
          break;
        case 7:
          this.explicacaoPelagem =
            "Tabby spotted: ao invés da presença de listras, ocorre a aparição de faixas em formato arredondado.";
          break;
        case 8:
          this.explicacaoPelagem =
            "Tortoise shell: possuem esse nome pois sua cor e formato assemelham-se com a dos casos de tartarugas. A combinação de cores mais comum nesse tipo de gato é a caramelo-preto.";
          break;
      }

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
  }
};
</script>
