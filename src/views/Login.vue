<template>
    <div class="d-flex justify-center">
        <v-card width="600px" class="mt-12 pa-10">
            <v-card-title>
                Войдите в аккаунт
            </v-card-title>

            <v-text-field
                label="Введите логин"
                v-model="login"
                outlined
            ></v-text-field>

            <v-text-field
                label="Введите пароль"
                v-model="password"
                type="password"
                outlined
            ></v-text-field>

            <v-btn v-on:click="auth">
                Войти
            </v-btn>
        </v-card>
    </div>
</template>

<script>
export default {
  name: 'Login',
  components: {
  },
  data() {
      return {
          password:'',
          login:''
      }
  },
  methods: {
    auth(){
      this.axios.get(`http://37.77.104.246/api/jsonstorage/?id=e42c3957000fa1d66e09c8b7f48c08fa`)
      .then((response) => {
        let done = false;
        for (let user of response.data) {
            if (this.login == user.login && this.password == user.password) {
                this.$emit('login', user)
                this.$router.push('/users/' + user.login)
                done = true;
                break;
            }
        }
        if (!done) {
            window.alert("Неверный логин или пароль")
        }
      })
    },
  },
  watch: {
      route() {

      }
  },
  mounted() {

  }
}
</script>
