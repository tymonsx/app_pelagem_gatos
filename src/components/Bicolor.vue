<template>
  <q-page :style-fn="myTweak">
    <p>
      Bicolor: São gatos que possuem pelagem de uma cor combinada com outra cor.
      A forma como esta combinação está presente no corpo pode variar
    </p>
    <img src="~assets/bicolor1.png" class="exemploGato" />
    <img src="~assets/bicolor2.png" class="exemploGato" />
    <img src="~assets/bicolor3.png" class="exemploGato" />
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
