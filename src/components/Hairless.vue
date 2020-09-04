<template>
  <q-page :style-fn="myTweak">
    <p>
      Hairless: possuem este nome pela quase completa ausência de pelagem.
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
