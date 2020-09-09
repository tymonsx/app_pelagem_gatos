<template>
  <q-page :style-fn="myTweak">
    <p>
      Solid color: Caracterizado por possuir uma cor única por toda a extensão
      do corpo.
    </p>
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
