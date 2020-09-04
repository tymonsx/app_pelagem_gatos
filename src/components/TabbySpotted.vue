<template>
  <q-page :style-fn="myTweak">
    <p>
      Tabby spotted: ao invés da presença de listras, ocorre a aparição de
      faixas em formato arredondado.
    </p>
    <img src="~assets/tabby_spotted_pattern.png" style="width:45%;" />
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
