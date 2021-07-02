<template>
  <div>
    <search-bar
      @filter-select_sortby="select_sortby = $event"
      @filter-select_categories="select_categories = $event"
      @filter-search="search = $event"
    ></search-bar>
    <item-list-home
      :search="search"
      :items="items"
      :select_sortby="select_sortby"
    ></item-list-home>
  </div>
</template>
<script>
import SearchBar from "../components/SearchBar.vue";
import ItemListHome from "../components/ItemListHome.vue";

export default {
  components: {
    SearchBar,
    ItemListHome,
  },
  data() {
    return {
      select_categories: [],
      select_sortby: "Recent",
      items: [],
      search: "",
    };
  },
  async fetch() {
    try {
      await this.$axios.get(`/api/items`).then((res) => {
        this.items = res.data;
      });
    } catch (e) {
      console.log(e);
    }
  },
};
</script>
<style lang="scss">
</style>