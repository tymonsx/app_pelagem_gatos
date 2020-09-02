<template>
  <q-page>
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
