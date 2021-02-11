<template>
  <q-page :style-fn="myTweak">
    <p
      :class="$q.screen.width > 1000 ? 'text-center' : 'text-justify'"
      style="margin-left: 0.8%; width:98%;"
    ></p>
    <p>
      Solid color: Caracterizado por possuir uma cor única por toda a extensão
      do corpo.
    </p>
    <img src="~assets/solid_color1.png" class="exemploGato" />
    <img src="~assets/solid_color2.png" class="exemploGato" />
    <img src="~assets/solid_color3.png" class="exemploGato" />
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
