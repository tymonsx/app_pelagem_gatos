<template>
  <q-layout>
      <q-page>
        <!--<div id="divFotoCamera">-->
          <video id="video">Video stream not available.</video>
          <canvas id="canvas"></canvas>
        <!--</div>-->
        <div id="divBotoes">
          <q-btn id="botaoTirarFoto" color="primary" @click="tirarFoto({stream})">Tirar foto</q-btn>
          <q-btn id="botaoReativarVideo" color="primary" @click="reativarVideo()">Reativar vídeo</q-btn>
        </div>
    </q-page>
  </q-layout>
</template>
<script>
import { Dialog } from 'quasar'

export default {
  data() {
    return {
      canvas: "",
      foto: "",
      stream: null
    };
  },
  mounted() {
    navigator.mediaDevices.getUserMedia({video: true, audio: false}).then(function(stream) {
      video.srcObject = stream;
      video.play();
      this.stream = stream;

      console.log("Stream 1", stream);
      return stream;
    }).then((stream) => {
        console.log("Stream 2", stream);
        this.tirarFoto(stream);
    });
  },
  methods: {
    reativarVideo() {

      document.getElementById("video").style.display = "block";
      console.log("display", document.getElementById("video").style.display);

      document.getElementById("canvas").style.display = "none";
      console.log("display", document.getElementById("canvas").style.display);

      navigator.mediaDevices.getUserMedia({video: true, audio: false}).then(function(stream) {
        video.srcObject = stream;
        video.play();

        console.log("Stream 1", stream);
        return stream;
      }).then((stream) => {
        console.log("Stream 2", stream );
        //this.tirarFoto(stream);
      }) 
      .catch(function(err) {
        console.log("An error occurred: " + err);
      });
    },
    tirarFoto(stream) {
        console.log("Stream 3", stream);
        document.getElementById("canvas").style.display = "block";
        console.log("display", document.getElementById("canvas").style.display);

        var context = canvas.getContext("2d");
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

      
      navigator.mediaDevices.getUserMedia({video: true, audio: false}).then(function(stream) {
        video.srcObject = stream;
        video.pause();

        stream.getTracks().forEach(function(track) {
          console.log("Stream 5");
          if (track.kind == "video") {
            console.log("Stream 6");
            track.stop();
          }
        });
      })
    }
  }
};
</script> 