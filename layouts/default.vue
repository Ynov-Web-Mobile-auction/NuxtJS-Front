<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :clipped="clipped"
      temporary
      fixed
      app
    >
    <v-list>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title>test</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-spacer></v-spacer>
      <NuxtLink to="/" class="logo">
        <v-avatar>
          <img src="../assets/img/logo.svg" alt="John" />
        </v-avatar>
        <v-toolbar-title class="title" v-text="title" />
      </NuxtLink>
      <v-spacer></v-spacer>
      <v-btn icon @click="modalShow = true">
        <v-icon class="icon _account">mdi-note-plus</v-icon>
      </v-btn>
      <v-btn icon to="/profil">
        <v-icon class="icon _account">mdi-account</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <item-modal v-if="modalShow" @close="modalShow = false" />
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>
<script>
import ItemModal from "../components/ItemModal.vue";

export default {
  components: { ItemModal },
  data() {
    return {
      modalShow: false,
      clipped: false,
      drawer: false,
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

.nuxt-link-active {
  color: inherit !important;
  text-decoration: none;
}
</style>