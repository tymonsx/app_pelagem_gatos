<template>
  <q-page class="flex flex-center">
    <AnalisePelagem />
  </q-page>
</template>

<script>
import AnalisePelagem from "components/AnalisePelagemCameraAPI.vue";
export default {
  name: "PageIndex",
  components: {
    AnalisePelagem
  }
};
</script>
