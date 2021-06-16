<template>
  <ItemForm @submitItem="putItem($event)"></ItemForm>
</template>
<script>
import ItemForm from "../components/ItemForm.vue";

export default {
  components: {
    ItemForm,
  },
  methods: {
    async putItem(item) {
      try {
        await this.$axios.post(`/api/items`, item).then(() => {
          this.$router.push({ name: "index" });
        });
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>
<style lang="scss">
</style>