<template>
  <q-page :style-fn="myTweak">
    <p
      :class="$q.screen.width > 1000 ? 'text-center' : 'text-justify'"
      style="margin-left: 0.8%; width:98%;"
    >
      Tabby spotted: Caracterizado pela separação das listras dos gatos tabby em
      manchas arredondadas. Os gatos tabby possuem uma marca característica em
      formato de "M" na testa.
    </p>
    <img src="~assets/tabby_spotted.png" class="exemploGato" />
    <img src="~assets/tabby_spotted2.png" class="exemploGato" />
    <img src="~assets/tabby_spotted3.png" class="exemploGato" />
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
