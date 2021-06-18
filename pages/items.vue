<template>
  <div class="item_page">
    <item-single v-if="item" :item="item"></item-single>
    <enchere-list v-if="encheres" :encheres="encheres"></enchere-list>
  </div>
</template>
<script>
import ItemSingle from "../components/ItemSingle.vue";
import EnchereList from "../components/EnchereList.vue";
export default {
  components: {
    ItemSingle,
    EnchereList,
  },
  methods: {},
  data() {
    return {
      item: "",
      encheres: "",
    };
  },
  async fetch() {
    try {
      await this.$axios
        .get(`/api/items/${this.$route.query.id}`)
        .then((res) => {
          this.item = res.data;
          this.$axios.get(`/api/auctions/${res.data.id}`).then((res2) => {
            this.encheres = res2.data;
          });
        });
    } catch (e) {
      console.log(e);
    }
  },
};
</script>
<style lang="scss">
.item_page {
  display: flex;
}
</style>