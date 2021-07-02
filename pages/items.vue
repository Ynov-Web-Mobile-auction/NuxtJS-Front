<template>
  <div class="item_page">
    <item-single class="item_p" v-if="item" :item="item"></item-single>
    <enchere-list
      class="list_ench"
      v-if="encheres"
      :encheres="encheres"
    ></enchere-list>
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
.item_p {
  margin-right: 30px;
}
.list_ench {
  margin-right: auto;
  margin-left: 30px;
  margin-top: 48px;
}

@media screen and (max-width: 992px) {
  .item_page {
    flex-direction: column;
  }

  .item_p {
    margin-right: auto;
  }
  .list_ench {
    margin-left: auto;
  }
}
</style>