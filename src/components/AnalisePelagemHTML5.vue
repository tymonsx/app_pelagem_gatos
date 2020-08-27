<template>
  <section>
    <q-modal v-model="opened">
      <section class="relative-position overflow-hidden fit">
        <figure class="no-margin" v-if="!imageUrl">
          <video
            ref="video"
            :src="source"
            class="fixed-center"
            :height="camHeight"
          />
        </figure>

        <div>
          <img
            v-if="bin.images.length > 0"
            class="rounded-borders border-primary avatar-lg absolute-bottom-right last-pic-avatar"
            :src="lastImg"
          />

          <loading v-if="loadingCamera">
            Loading...
          </loading>

          <img
            v-if="imageUrl"
            class="window-width"
            :src="imageUrl"
            alt="Image taken"
          />

          <cam-btn-group class="no-shadow bg-black flat">
            <div v-if="imageUrl">
              <q-btn
                @click="onConfirmImage"
                class="absolute-center"
                flat
                color="white"
                icon="far fa-check-circle"
                size="xl"
              />
              <q-page-sticky position="bottom-right" :offset="[10, -54]">
                <q-btn
                  @click="onCancelImage"
                  class="q-ml-xl"
                  flat
                  color="white"
                  icon="far fa-times-circle"
                  size="xl"
                  wait-for-ripple
                />
              </q-page-sticky>
            </div>
            <div v-else>
              <q-btn
                @click="onCapture"
                class="absolute-center"
                flat
                color="white"
                icon="far fa-dot-circle"
                size="xl"
              />

              <q-page-sticky position="bottom-right" :offset="[10, -60]">
                <q-btn
                  @click="exitCamera"
                  label="Next"
                  wait-for-ripple
                  flat
                  color="white"
                  icon-right="fas fa-long-arrow-alt-right"
                  size="xl"
                />
              </q-page-sticky>
            </div>
          </cam-btn-group>
        </div>
      </section>
    </q-modal>
  </section>
</template>

<script>
import { get } from "vuex-pathify";
import messages from "../../common/messages.json";
import Loading from "../VLoading";
import CamBtnGroup from "../VFooterBtns.vue";

export default {
  name: "Camera",
  components: {
    Loading,
    CamBtnGroup
  },
  data() {
    return {
      opened: true,
      mediaStream: null,
      imageUrl: null,
      isDefaultBackCamera: true,
      camera: null,
      cameras: [],
      source: null,
      loadingCamera: true
    };
  },
  computed: {
    ...get("DeployModule/*"),
    hasBackCamera() {
      const backCameraDevices = this.cameras.filter(device => {
        return device.label.indexOf("back") !== -1;
      });
      return backCameraDevices.length > 1 ? backCameraDevices[0] : false;
    },
    camHeight() {
      return window.innerHeight;
    },
    lastImg() {
      return this.bin.images.slice(-1);
    }
  },
  mounted() {
    if (navigator.mediaDevices === undefined) {
      navigator.mediaDevices = {};
    }

    if (navigator.mediaDevices.getUserMedia === undefined) {
      navigator.mediaDevices.getUserMedia = this.legacyGetUserMediaSupport();
    }

    let constraints = this.isDefaultBackCamera ? "environment" : "user";
    constraints = { video: { facingMode: { ideal: constraints } } };

    this.testMediaAccess(constraints);
  },
  methods: {
    legacyGetUserMediaSupport() {
      return constraints => {
        // First get ahold of the legacy getUserMedia, if present
        let getUserMedia =
          navigator.getUserMedia ||
          navigator.webkitGetUserMedia ||
          navigator.mozGetUserMedia ||
          navigator.msGetUserMedia ||
          navigator.oGetUserMedia;

        // Some browsers just don't implement it - return a rejected promise with an error
        // to keep a consistent interface
        if (!getUserMedia) {
          return Promise.reject(
            new Error("getUserMedia is not implemented in this browser")
          );
        }

        // Otherwise, wrap the call to the old navigator.getUserMedia with a Promise
        return new Promise(function(resolve, reject) {
          getUserMedia.call(navigator, constraints, resolve, reject);
        });
      };
    },
    testMediaAccess(constraints) {
      // Check if there's the camera set by isDefaultBackCamera
      navigator.mediaDevices
        .getUserMedia(constraints)
        .then(stream => {
          this.getCameras();
        })
        .catch(() => {
          this.$q.notify(messages.camera.error.backCamera);
          this.testMediaAccess({ video: true });
        });
    },
    getCameras() {
      // GET The cameras && and get the Back Camera
      navigator.mediaDevices.enumerateDevices().then(deviceInfos => {
        this.loadingCamera = false;
        deviceInfos.forEach(device => {
          const constraints = this.hasBackCamera ? "back" : "amera"; // Camera string could be Capital

          if (device.label.indexOf(constraints) !== -1) {
            this.camera = device;
          }

          if (device.kind.indexOf("videoinput") !== -1) {
            this.cameras.push(device);
          }
        });
        this.setCamera(this.camera.deviceId);
      });
    },
    setCamera(deviceId) {
      navigator.mediaDevices
        .getUserMedia({ video: { deviceId: { exact: deviceId } } })
        .then(mediaStream => {
          this.mediaStream = mediaStream;
          /** Load the stream to the video tag**/
          if ("srcObject" in this.$refs.video) {
            // new browsers api
            this.$refs.video.srcObject = mediaStream;
            this.$refs.video.onloadedmetadata = () => {
              this.$refs.video.play();
            };
          } else {
            // old broswers
            this.mediaStream = window.HTMLMediaElement.srcObject(mediaStream);
          }
        })
        .catch(() => this.$q.notify(messages.camera.error.camera));
    },
    onCapture() {
      const mediaStreamTrack = this.mediaStream.getVideoTracks()[0];
      const imageCapture = new window.ImageCapture(mediaStreamTrack);

      return imageCapture.takePhoto().then(blob => {
        this.imageUrl = URL.createObjectURL(blob);
      });
    },
    onConfirmImage() {
      this.bin.images.push(this.imageUrl);
      this.$store.set("DeployModule/bin@images", this.bin.images);
      this.imageUrl = null;
      this.setCamera(this.camera.deviceId);
    },
    onCancelImage() {
      this.imageUrl = null;
      this.setCamera(this.camera.deviceId);
    },
    exitCamera() {
      let stream = this.$refs.video.srcObject;
      let tracks = stream.getTracks();

      tracks.forEach(track => {
        // stops the video track
        track.stop();
      });
      this.$refs.video.srcObject = null;
      this.mediaStream = null;

      this.$emit("stopped");

      this.opened = false;
    }
  }
};
</script>

<style lang="stylus" scoped>
.icon-group .wrapper-icon
    font-size 36px

.inner-icon
    position relative
    font-size 20px
    top 4px
    left -54px
    z-index 99

.last-pic-avatar
    margin 0 60px 70px 0
    z-index 9999999999

.arrow-exit
    position absolute
    left 0
    top 5px
</style>
