<template>
  <q-page :style-fn="myTweak">
    <p>
      Tortoiseshell: Possuem trechos em sua pelagem com gradações de laranja e
      preto. O tamanho destes trechos podem variar de um salpicado até grandes
      áreas de uma única cor. Estas áreas costumam ter um formato assimétrico.
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
