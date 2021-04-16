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
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
    <v-app-bar-nav-icon @click.stop="drawer = !drawer"/>
    <v-spacer></v-spacer>
    <NuxtLink to="/" class="logo">
        <v-avatar>
        <img
            src="../assets/img/logo.svg"
            alt="John"
        >
        </v-avatar>
        <v-toolbar-title class="title" v-text="title"/>
    </NuxtLink>
    <v-spacer></v-spacer>
    <v-btn icon to="/profil">
        <v-icon class="icon _account">mdi-account</v-icon>
    </v-btn>
    
    </v-app-bar>
    <v-main>
        <v-container>
            <nuxt/>
        </v-container>
    </v-main>
    
  </v-app>
</template>
<script>
export default {
    data() {
        return {
            clipped: false,
            drawer: false,
            title: 'PVAE'
        }
    },
}
</script>
<style lang="scss">
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
    .v-icon {
        &._account {
            // font-size: 30px;
        }
    }


    .nuxt-link-active {
        color: inherit !important;
        text-decoration: none;
    }
</style>