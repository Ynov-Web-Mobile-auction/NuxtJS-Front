<template>
  <div>
    <search-bar
      @filter-select_sortby="select_sortby = $event"
      @filter-select_categories="select_categories = $event"
      @filter-search="search = $event"
    ></search-bar>
    <item-list
      :search="search"
      :items="items"
      :select_sortby="select_sortby"
    ></item-list>
  </div>
</template>
<script>
import SearchBar from "../components/SearchBar.vue";
import ItemList from "../components/ItemList.vue";

export default {
  components: {
    SearchBar,
    ItemList,
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