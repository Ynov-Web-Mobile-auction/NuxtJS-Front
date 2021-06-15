<template>
  <div class="items">
    <item-card
      v-for="item in filteredList"
      :key="item.id"
      :item="item"
    ></item-card>
  </div>
</template>
<script>
import ItemCard from "./ItemCard.vue";

export default {
  components: {
    ItemCard,
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
            post.name
              .toLowerCase()
              .normalize("NFD")
              .replace(/[\u0300-\u036f]/g, "")
              .includes(word)
          )
        )
        .sort((p1, p2) => {
          switch (this.select_sortby) {
            case "Lowest Price":
              return p1.price - p2.price;
            case "Highest Price":
              return p2.price - p1.price;
            case "Recent":
              return p2.id - p1.id;
            case "Oldest":
              return p1.id - p2.id;
            default:
              return 0;
          }
        })
        .map((post) => {
          const nameFormated = this.searchWords.length
            ? post.name.replace(
                new RegExp(this.searchWords.join("|"), "gi"),
                '<span class="highlight">$&</span>'
              )
            : post.name;
          return {
            ...post,
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