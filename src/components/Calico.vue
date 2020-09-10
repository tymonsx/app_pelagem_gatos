<template>
  <q-page :style-fn="myTweak">
    <p>
      Calico: Possuem de 25% a 75% da cor branca e combinação de laranja e
      preto. Porém podem variar para trechos de creme e cinza.
    </p>
    <img src="~assets/calico1.png" class="exemploGato" />
    <img src="~assets/calico2.png" class="exemploGato" />
    <img src="~assets/calico3.png" class="exemploGato" />
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
