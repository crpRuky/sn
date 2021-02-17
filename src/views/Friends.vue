<template>
  <v-container class="d-flex flex-wrap justify-center">
    <user-card v-for="(user, i) in userList" :key="i" :username="user.name" :city="user.city" :id="user.login" :image="user.photo"></user-card>
  </v-container>
</template>

<script>
import UserCard from '../components/UserCard.vue'

export default {
  name: 'Friends',
  components: {
      UserCard
  },
  data() {
      return {
          id: this.$route.params.id,
          userList:[],
          photos:[]
      }
  },
  methods: {
    getUsers(){
      this.axios.get(`https://api.npoint.io/77ea9f8e27a6895be323`)
      .then((response) => {
        this.userList = response.data;
      })
    },
  },
  watch: {
      route() {
        this.getUsers();
      }
  },
  mounted() {
      this.getUsers();
  }
}
</script>
