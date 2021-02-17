<template>
    <v-container align="center" justify="center">
        <v-row class="text-left">
            <v-col cols="10">
                <h1 class="green--text text--darken-2">
                    <v-icon large color="green darken-2">mdi-account-outline</v-icon>
                    {{page_user.name}}
                </h1>
            </v-col>
        </v-row>
        <v-row class="text-left">
            <v-col cols="2">
                <img :src="page_user.photo" style="max-width: 100%">
            </v-col>
            <v-col cols="10" class="text-left" max-width="400">
                <p>
                    Веб-сайт: <a href="https://example.com" target="_blank">{{page_user.website}}</a>
                </p>
                <p>
                    E-mail: <a href="mailto:...">{{page_user.email}}</a>
                </p>
                <p>
                    Город: {{page_user.city}}
                </p>
                <p v-if="page_user.company != ''">
                    Место работы: {{page_user.company}}
                </p>
            </v-col>
        </v-row>

        <v-divider style="margin:30px 0px 50px 0px"></v-divider>

        <profile-card v-for="(post, i) in posts" v-bind:key="i" :image="page_user.photo" :author="page_user.name" :likes="post.likes">
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
          page_user:JSON,
          posts:[]
      }
  },
  methods: {
    getUser(){
      this.axios.get(`http://37.77.104.246/api/jsonstorage/?id=e42c3957000fa1d66e09c8b7f48c08fa`)
      .then((response) => {
        for (let user of response.data) {
            if (user.login == this.id) {
                this.page_user = user;
                break;
            }
        }
      })
    },
    getUserPosts(){
        this.axios.get(`http://37.77.104.246/api/jsonstorage/?id=0cbd142cb7084279fa79dda38caac266`)
        .then((response) => {
            for (let user of response.data) {
                if (user.login == this.id) {
                    this.posts = user.posts;
                    break;
                }
            }
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
