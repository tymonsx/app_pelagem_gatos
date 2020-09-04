<template>
  <q-page :style-fn="myTweak">
    <p>
      Bicolor: geralmente possuem uma cor predominamente branca. A cor
      secundária pode estar presente em formato de manchas aleatórias
      ('magpie'), manchas aleatórias com cauda colorida ('harlequin') ou manchas
      coloridas na cabeça e nas costas (van).
    </p>
    <img src="~assets/bicolor_patterns.png" style="width:90%;" />
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
