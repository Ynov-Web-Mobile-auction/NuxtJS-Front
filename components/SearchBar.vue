<template>
  <div class="search_box">
    <v-text-field
      @input="$emit('filter-search', $event)"
      class="search"
      label="Search items"
    ></v-text-field>
    <div class="options">
      <v-select
        @change="$emit('filter-select_sortby', $event)"
        class="select sortby"
        :items="items_sortby"
        label="Sort by"
        outlined
      ></v-select>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      items_sortby: [
        "Recent",
        "Oldest",
        "Lowest Price",
        "Highest Price",
      ],
    };
  },
};
</script>
<style lang="scss">
.search_box {
  margin-top: 12px;
  display: flex;
  .options {
    margin-left: auto;
    display: flex;
    .select {
      &.categories {
        max-width: 330px;
        margin-right: 30px;
      }
      &.sortby {
        max-width: 176px;
      }
    }
  }
  .search {
    margin-right: 20px;
    margin-top: 11px;
  }
}

@media screen and (max-width: 800px) {
  .search_box {
    flex-direction: column;
    .options {
      margin-left: 0;
      .select {
        &.categories {
          max-width: none;
        }
      }
    }
    .search {
      max-width: none;
      margin-right: 0px;
    }
  }
}

@media screen and (max-width: 500px) {
  .search_box {
    .options {
      flex-direction: column;
      .select {
        &.categories {
          margin-right: 0px;
        }
        &.sortby {
          max-width: none;
        }
      }
    }
  }
}
</style>
