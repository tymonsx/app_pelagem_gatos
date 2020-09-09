<template>
  <q-page :style-fn="myTweak">
    <p>
      Tabby spotted: Caracterizado pela separação das listras dos gatos tabby em
      manchas arredondadas. Os gatos tabby possuem uma marca característica em
      formato de "M" na testa.
    </p>
    <!--<img src="~assets/tabby_spotted_pattern.png" style="width:45%;" />-->
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
