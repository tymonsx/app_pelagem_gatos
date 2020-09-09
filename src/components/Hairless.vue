<template>
  <q-page :style-fn="myTweak">
    <p>
      Hairless: Possuem este nome pela falta de pêlos.
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
