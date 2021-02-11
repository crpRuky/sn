<template>
  <v-app id="app">
    <v-navigation-drawer
      app
      color="green"
      dark
      expand-on-hover
      hide-overlay
      permanent
      right
    >

      <v-list nav shaped dense>

        <v-list-item two-line>
          <v-list-item-avatar style="margin-left: -8px; margin-right: 23px">
            <img src="https://randomuser.me/api/portraits/men/7.jpg">
          </v-list-item-avatar>
          <v-list-item-content class="text-left">
            <v-list-item-title class="font-weight-black">Иван Иванов</v-list-item-title>
            <v-list-item-subtitle>Я не знаю кто это</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>

        <v-divider class="my-3"></v-divider>

        <v-list-item link to="/">
          <v-list-item-icon>
            <v-icon>mdi-home-outline</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="text-left">Главная</v-list-item-title>
          </v-list-item-content>
        </v-list-item>



        <v-list-item link to="/login" v-if="!current_user">
          <v-list-item-icon>
            <v-icon>mdi-account-arrow-left-outline</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="text-left">Вход</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item exact link :to="'/users/' + current_user.login" v-else>
          <v-list-item-icon>
            <v-icon>mdi-account-arrow-left-outline</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="text-left">Профиль</v-list-item-title>
          </v-list-item-content>
        </v-list-item>



        <v-list-item link to="/users" exact>
          <v-list-item-icon>
            <v-icon>mdi-account-plus-outline</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="text-left">Найти друзей</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

      </v-list>

    </v-navigation-drawer>

    <v-content class="px-12 py-3">
      <v-container fluid>
        <router-view v-on:login="updateUser($event)" />
      </v-container>
    </v-content>

  </v-app>
</template>

<script>
export default {
  name: 'App',

  components: {
  },

  data: () => {
    return {
      navigation: true,
      current_user:null
    }
  },

  methods: {
    updateUser(user) {
      this.current_user = user; 
    }
  }
};
</script>
