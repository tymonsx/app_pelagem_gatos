<template>
  <q-layout>
    <q-page class="">
      <div class="full-width text-center q-ma-sm">
        <video id="video">Video stream not available.</video>
        <canvas id="canvas" />
      </div>
      <div id="divBotoes" class="full-width text-center">
        <q-btn id="botaoTirarFoto" color="primary" @click="irarFoto({ stream })"
          >Tirar foto</q-btn
        >
        <q-btn id="botaoReativarVideo" color="primary" @click="reativarVideo()"
          >Reativar vĂ­deo</q-btn
        >
      </div>
    </q-page>
  </q-layout>
</template>
<style scoped>
/* telas maiores */

#video {
  width: 500px;
  height: 375px;
  display: inline-block;
}

#canvas {
  width: 500px;
  height: 375px;
  display: none;
}

/* telas menores*/
</style>
<script>
import { Dialog } from "quasar";

export default {
  data() {
    return {
      canvas: "",
      foto: "",
      stream: null,
      height: 1080,
      width: 1920,
      aspect: 16 / 9
    };
  },
  mounted() {
    this.width = this.height * this.aspect;
    const video = document.getElementById("video");
    const canvas = document.getElementById("canvas");
    canvas.width = video.width = this.width;
    canvas.height = video.height = this.height;

    navigator.mediaDevices
      .getUserMedia({ video: true, audio: false })
      .then(function(stream) {
        video.srcObject = stream;
        video.play();
        this.stream = stream;

        console.log("Stream 1", stream);
        return stream;
      })
      .then(stream => {
        console.log("Stream 2", stream);
        this.tirarFoto(stream);
      });
  },
  methods: {
    reativarVideo() {
      document.getElementById("video").style.display = "inline-block";
      console.log("display", document.getElementById("video").style.display);

      document.getElementById("canvas").style.display = "none";
      console.log("display", document.getElementById("canvas").style.display);

      navigator.mediaDevices
        .getUserMedia({ video: true, audio: false })
        .then(function(stream) {
          video.srcObject = stream;
          video.play();

          console.log("Stream 1", stream);
          return stream;
        })
        .then(stream => {
          console.log("Stream 2", stream);
          //this.tirarFoto(stream);
        })
        .catch(function(err) {
          console.log("An error occurred: " + err);
        });
    },
    irarFoto(stream) {
      console.log("Stream 3", stream);
      document.getElementById("canvas").style.display = "inline-block";
      console.log("display", document.getElementById("canvas").style.display);

      var context = canvas.getContext("2d");
      //context.imageSmoothingEnabled = false;
      context.drawImage(video, 0, 0, canvas.width, canvas.height);
      var data = canvas.toDataURL();
      //foto.setAttribute("src", data);
      //console.log(data);
      //console.log("foto", foto);
      this.pausarVideo(stream);
    },
    pausarVideo(stream) {
      console.log("Stream 4", stream);
      document.getElementById("video").style.display = "none";
      console.log("display", document.getElementById("video").style.display);

      navigator.mediaDevices
        .getUserMedia({ video: true, audio: false })
        .then(function(stream) {
          video.srcObject = stream;
          video.pause();

          stream.getTracks().forEach(function(track) {
            console.log("Stream 5");
            if (track.kind == "video") {
              console.log("Stream 6");
              track.stop();
            }
          });
        });
    }
  }
};
</script>
