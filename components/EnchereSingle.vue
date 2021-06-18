<template>
  <v-card>
    <v-card-text class="enchere_single"
      >{{ enchere.price }} ETH - {{ user.name }} -
      {{ enchere.created_at }}</v-card-text
    >
  </v-card>
</template>
<script>
export default {
  data() {
    return {
      user: "",
    };
  },
  props: {
    enchere: {
      type: Object,
      default() {
        return {};
      },
    },
  },
  async fetch() {
    try {
      await this.$axios
        .get(`/api/users/${this.enchere.user_id}`)
        .then((res) => {
          this.user = res.data;
        });
    } catch (e) {
      console.log(e);
    }
  },
};
</script>
<style lang="scss">
.enchere_single {
  margin-bottom: 10px;
}
</style>
