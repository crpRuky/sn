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

        <!-- main -->
        <v-list-item two-line>
          <v-list-item-avatar style="margin-left: -8px; margin-right: 23px">
            <img :src="current_user.photo">
          </v-list-item-avatar>
          <v-list-item-content class="text-left">
            <v-list-item-title class="font-weight-black">{{current_user.name}}</v-list-item-title>
            <v-list-item-subtitle>{{current_user.city}}</v-list-item-subtitle>
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


        <!-- log -->
        <v-list-item link to="/login" v-if="current_user.not_logged">
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
        
        <!-- reg -->
        <v-list-item link to="/registration" v-if="current_user.not_logged">
          <v-list-item-icon>
            <v-icon>mdi-account-plus-outline</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="text-left">Регистрация</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <!-- find -->
        <v-list-item link to="/users" exact>
          <v-list-item-icon>
            <v-icon>mdi-account-search-outline</v-icon>
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
      current_user: {
        name:"Войдите в аккаунт",
        city:"",
        photo:"https://cdn4.iconfinder.com/data/icons/linecon/512/photo-512.png",
        not_logged:true
      }
    }
  },

  methods: {
    updateUser(user) {
      this.current_user = user; 
    }
  }
};
</script>
