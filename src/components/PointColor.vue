<template>
  <q-page :style-fn="myTweak">
    <p>
      Point color: São caracterizados por possuirem cores mais escuras na face,
      orelha, pés e cauda e uma versão mais clara da mesma cor no resto do corpo
      e também podem possuir um pouco de branco.
    </p>
    <img src="~assets/point_color1.png" class="exemploGato" />
    <img src="~assets/point_color2.png" class="exemploGato" />
    <img src="~assets/point_color3.png" class="exemploGato" />
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
