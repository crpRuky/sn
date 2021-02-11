<template>
  <v-container class="d-flex flex-wrap justify-center">
    <user-card v-for="(user, i) in userList" :key="i" :username="user.name" :city="user.address.city" :id="i"></user-card>
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
      this.axios.get(`http://jsonplaceholder.typicode.com/users`)
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
