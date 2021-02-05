<template>
  <q-page :style-fn="myTweak">
    <p
      :class="$q.screen.width > 1000 ? 'text-center' : 'text-justify'"
      style="margin-left: 0.8%; width:98%;"
    >
      Tabby classic: Possuem listras largas em formato de redemoinho fazendo com
      que a lateral do corpo lembre um alvo. Os gatos tabby possuem uma marca
      característica em formato de "M" na testa.
    </p>
    <img src="~assets/tabby_classic.png" class="exemploGato" />
    <img src="~assets/tabby_classic2.png" class="exemploGato" />
    <img src="~assets/tabby_classic3.png" class="exemploGato" />
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
