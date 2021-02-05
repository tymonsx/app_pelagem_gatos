<template>
  <q-page :style-fn="myTweak">
    <p
      :class="$q.screen.width > 1000 ? 'text-center' : 'text-justify'"
      style="margin-left: 0.8%; width:98%;"
    >
      Tortoiseshell: Possuem trechos em sua pelagem com gradações de laranja e
      preto. O tamanho destes trechos podem variar de um salpicado até grandes
      áreas de uma única cor. Estas áreas costumam ter um formato assimétrico.
    </p>
    <img src="~assets/tortoise_shell1.png" class="exemploGato" />
    <img src="~assets/tortoise_shell2.png" class="exemploGato" />
    <img src="~assets/tortoise_shell3.png" class="exemploGato" />
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
