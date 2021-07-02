<template>
  <div class="items">
    <item-single
      v-for="item in filteredList"
      :key="item.id"
      :item="item"
      pos="view"
    ></item-single>
  </div>
</template>
<script>
import ItemSingle from "./ItemSingle.vue";

export default {
  components: {
    ItemSingle,
  },
  props: {
    items: {
      type: Array,
      default() {
        return [];
      },
    },
    select_sortby: { type: String, default: "" },
    search: { type: String, default: "" },
  },
  computed: {
    searchWords() {
      return this.search.toLowerCase().split(" ");
    },
    filteredList() {
      return this.items
        .filter((post) =>
          this.searchWords.every((word) =>
            post.item.name
              .toLowerCase()
              .normalize("NFD")
              .replace(/[\u0300-\u036f]/g, "")
              .includes(word)
          )
        )
        .sort((p1, p2) => {
          switch (this.select_sortby) {
            case "Lowest Price":
              return p1.item.price - p2.item.price;
            case "Highest Price":
              return p2.item.price - p1.item.price;
            case "Recent":
              return p2.item.id - p1.item.id;
            case "Oldest":
              return p1.item.id - p2.item.id;
            default:
              return 0;
          }
        })
        .map((post) => {
          const nameFormated = this.searchWords.length
            ? post.item.name.replace(
                new RegExp(this.searchWords.join("|"), "gi"),
                '<span class="highlight">$&</span>'
              )
            : post.item.name;
          return {
            ...post.item,
            nameFormated,
          };
        });
    },
  },
};
</script>
<style lang="scss">
.items {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>