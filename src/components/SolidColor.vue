<template>
  <q-page :style-fn="myTweak">
    <p>
      Solid color: possuem somente uma cor por toda a sua extensão.
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
