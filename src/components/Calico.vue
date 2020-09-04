<template>
  <q-page :style-fn="myTweak">
    <p>
      Calico: com bastantes semelhanças ao tortoise shell, sua principal
      diferença é a presença da tonalidade branca.
    </p>
  </q-page>
</template>
<script>
export default {
  methods: {
    myTweak(offset) {
      return { minHeight: null };
    }
  }
};
</script>
