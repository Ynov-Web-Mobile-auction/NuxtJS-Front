<template>
  <v-app dark>
    <v-app-bar class="navbar" fixed app>
      <NuxtLink to="/" class="logo">
        <v-avatar>
          <img src="../assets/img/logo.svg" alt="John" />
        </v-avatar>
        <v-toolbar-title class="title" v-text="title" />
      </NuxtLink>
      <v-spacer></v-spacer>
      <v-tooltip bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            class="btn_nav"
            v-bind="attrs"
            v-on="on"
            icon
            @click="modalShow = true"
          >
            <v-icon class="icon _account">mdi-note-plus</v-icon>
          </v-btn>
        </template>
        <span>Create Item</span>
      </v-tooltip>
      <v-tooltip bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn class="btn_nav" v-bind="attrs" v-on="on" icon to="/myitems">
            <v-icon class="icon _account">mdi-note-text</v-icon>
          </v-btn>
        </template>
        <span>My Items</span>
      </v-tooltip>
      <v-tooltip bottom>
        <template v-slot:activator="{ on, attrs }">
          <v-btn class="btn_nav" v-bind="attrs" v-on="on" icon to="/profil">
            <v-icon class="icon _account">mdi-account</v-icon>
          </v-btn>
        </template>
        <span>Account</span>
      </v-tooltip>
    </v-app-bar>
    <v-main>
      <Notification v-if="notif" :notif="notif" @close-notif="notif = null" />
      <create-item-modal @notif="assignAndWait($event)" v-if="modalShow" @close="modalShow = false" />
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>
<script>
import CreateItemModal from "../components/CreateItemModal.vue";
import Notification from "../components/Notification.vue";

export default {
  components: {
    CreateItemModal,
    Notification,
  },
  data() {
    return {
      modalShow: false,
      title: "PVAE",
      notif: null,
    };
  },
  methods: {
    assignAndWait(notif) {
      console.log("notif");
      this.notif = notif;
      setTimeout(() => {
        this.notif = null;
      }, 3000);
    },
  },
};
</script>
<style lang="scss">
a {
  text-decoration: none;
  color: inherit !important;
}
.navbar {
  padding-right: 8px;

  .btn_nav {
    margin: 0 5px;
  }
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