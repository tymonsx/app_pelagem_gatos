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

        <p id="msg"></p>
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
export default {
  data() {
    return {
      height: 250,
      width: 250,
      aspect: 16 / 9
    };
  },
  mounted() {
    // this.width = this.height * this.aspect;
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
          //document.getElementById("photo").class = "photo";
        },
        msg => {
          //falha
          document.getElementById("msg").textContent = msg;
        },
        opts
      );
    }
  }
};
</script>
