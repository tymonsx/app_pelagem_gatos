<template>
  <q-page :style-fn="myTweak">
    <p>
      Tabby classic: possuem listras largas na cor preta e geralmente sua cor
      predominamente é mais clara. Há também a presença de uma espécie de
      "redemoinho" em sua pelagem.
    </p>
    <img src="~assets/tabby_classic_pattern.png" style="width: 45%;" />
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
