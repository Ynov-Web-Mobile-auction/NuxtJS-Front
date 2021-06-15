<template>
  <item-single :item="item"></item-single>
</template>
<script>
import ItemSingle from "../components/ItemSingle.vue";
export default {
  components: {
    ItemSingle,
  },
  methods: {},
  data() {
    return {
      item: "",
    };
  },
  async fetch() {
    try {
      await this.$axios
        .get(`/api/items/${this.$route.query.id}`)
        .then((res) => {
          this.item = res.data;
        });
    } catch (e) {
      console.log(e);
    }
  },
};
</script>
<style lang="scss">
</style>