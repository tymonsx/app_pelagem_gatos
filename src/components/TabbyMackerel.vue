<template>
  <q-page :style-fn="myTweak">
    <p>
      Tabby mackerel: possuem listras verticais e mais finas que as do "tabby
      classic".
    </p>
    <img src="~assets/tabby_mackerel_pattern.png" style="width: 45%;" />
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
