<template>
  <q-page :style-fn="myTweak">
    <p>
      Exemplos de como bater a foto:
    </p>
    <div class="text-center">
      <img src="~assets/foto_sim1.png" class="exemploFotos" /><br />
      <img src="~assets/foto_sim2.jpg" class="exemploFotos" /><br />
      <img src="~assets/foto_sim3.png" class="exemploFotos" /><br />
    </div>
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
