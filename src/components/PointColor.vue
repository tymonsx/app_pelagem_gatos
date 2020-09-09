<template>
  <q-page :style-fn="myTweak">
    <p>
      Point color: São caracterizados por possuirem cores mais escuras na face,
      orelha, pés e cauda e uma versão mais clara da mesma cor no resto do corpo
      e também podem possuir um pouco de branco.
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
