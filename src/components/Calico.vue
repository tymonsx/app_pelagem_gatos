<template>
  <q-page :style-fn="myTweak">
    <p>
      Calico: Possuem de 25% a 75% da cor branca e combinação de laranja e
      preto. Porém podem variar para trechos de creme e cinza.
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
