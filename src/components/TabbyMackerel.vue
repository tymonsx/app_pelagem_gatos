<template>
  <q-page :style-fn="myTweak">
    <p>
      Tabby mackerel: Possuem um padrão de listras delgadas levemente curvas na
      lateral do corpo ou quebradas em segmentos de manchas. Os gatos tabby
      possuem uma marca característica em formato de "M" na testa.
    </p>
    <!--<img src="~assets/tabby_mackerel_pattern.png" style="width: 45%;" />-->
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
