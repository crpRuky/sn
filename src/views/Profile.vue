<template>
    <v-container align="center" justify="center">
        <v-row class="text-left">
            <v-col cols="10">
                <h1 class="green--text text--darken-2">
                    <v-icon large color="green darken-2">mdi-account-outline</v-icon>
                    {{username}}
                </h1>
            </v-col>
        </v-row>
        <v-row class="text-left">
            <v-col cols="2">
                <img :src="'https://randomuser.me/api/portraits/men/' + (id - 1) + '.jpg'" style="max-width: 100%">
            </v-col>
            <v-col cols="10" class="text-left" max-width="400">
                <p>
                    Веб-сайт: <a href="https://example.com" target="_blank">{{website}}</a>
                </p>
                <p>
                    E-mail: <a href="mailto:...">{{email}}</a>
                </p>
                <p>
                    Город: {{city}}
                </p>
                <p>
                    Место работы: {{company}}
                </p>
            </v-col>
        </v-row>

        <v-divider style="margin:30px 0px 50px 0px"></v-divider>

        <profile-card v-for="(post, i) in posts" v-bind:key="i" :author="username" :likes="256" :shares="64" :id="id - 1">
          <template v-slot:title>{{post.title}}</template>
          {{post.body}}
        </profile-card>

        <hr style="background-color:transparent; border:none; height:50px">


    </v-container>
</template>

<script>
import ProfileCard from '../components/ProfileCard.vue'

export default {
  name: 'Profile',
  components: {
    ProfileCard
  },
  data() {
      return {
          id: this.$route.params.id,
          username:'',
          website:'',
          email:'',
          city:'',
          company:'',
          posts:[]
      }
  },
  methods: {
    getUser(){
      this.axios.get(`http://jsonplaceholder.typicode.com/users/${this.id}`)
      .then((response) => {
        this.username = response.data.name;
        this.website = response.data.website;
        this.email = response.data.email;
        this.city = response.data.address.city;
        this.company = response.data.company.name;
      })
    },
    getUserPosts(){
        this.axios.get(`http://jsonplaceholder.typicode.com/posts?userId=${this.id}`)
        .then((response) => {
            this.posts = response.data;
        })
    }
  },
  watch: {
      route() {
        this.getUser();
        this.getUserPosts();
      }
  },
  mounted() {
      this.getUser();
      this.getUserPosts();
  }
}
</script>
