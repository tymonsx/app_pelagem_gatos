<template>
  <q-page :style-fn="myTweak">
    <p>
      Tortoiseshell: possuem esse nome pois sua cor e formato assemelham-se com
      a dos casos de tartarugas. A combinação de cores mais comum nesse tipo de
      gato é a caramelo-preto.
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
