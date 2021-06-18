<template>
  <v-app dark>
    <v-app-bar fixed app>
      <NuxtLink to="/" class="logo">
        <v-avatar>
          <img src="../assets/img/logo.svg" alt="John" />
        </v-avatar>
        <v-toolbar-title class="title" v-text="title" />
      </NuxtLink>
      <v-spacer></v-spacer>
      <v-btn icon to="/myitems">
        <v-icon class="icon _account">mdi-note-text</v-icon>
      </v-btn>
      <v-btn icon @click="modalShow = true">
        <v-icon class="icon _account">mdi-note-plus</v-icon>
      </v-btn>
      <v-btn icon to="/profil">
        <v-icon class="icon _account">mdi-account</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <create-item-modal v-if="modalShow" @close="modalShow = false" />
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>
<script>
import CreateItemModal from "../components/CreateItemModal.vue";

export default {
  components: { CreateItemModal },
  data() {
    return {
      modalShow: false,
      title: "PVAE",
    };
  },
};
</script>
<style lang="scss">
a {
  text-decoration: none;
  color: inherit !important;
}
.logo {
  display: flex;
  .v-avatar {
    margin: 0 5px 0 20px;
  }
  .title {
    align-items: center;
    display: flex;
  }
}
</style>