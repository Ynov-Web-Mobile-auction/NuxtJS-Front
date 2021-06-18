<template>
  <div>
    <enchere-single
      v-for="enchere in encheres.bids"
      :key="enchere.id"
      :enchere="enchere"
    ></enchere-single>
  </div>
</template>
<script>
import EnchereSingle from "./EnchereSingle.vue";

export default {
  components: {
    EnchereSingle,
  },
  props: {
    encheres: {
      type: Object,
      default() {
        return {};
      },
    },
  },
};
</script>
<style lang="scss">
</style>
