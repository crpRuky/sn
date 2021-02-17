<template>
    <div class="d-flex justify-center">
        <v-card width="650px" class="mt-12 pa-10">
            <v-card-title>
                Создать новый аккаунт
            </v-card-title>

            <v-row class="pl-2 pr-2 mt-2">
                <v-text-field
                    label="Имя"
                    v-model="name"
                    type="name"
                    outlined
                    class="mr-1"
                ></v-text-field>
                <v-text-field
                    label="Email"
                    v-model="email"
                    type="email"
                    outlined
                    class="ml-1"
                ></v-text-field>
            </v-row>

            <v-row class="pl-2 pr-2 mb-2">
                <v-text-field
                    label="Логин"
                    v-model="login"
                    outlined
                    class="mr-1"
                ></v-text-field>

                <v-text-field
                    label="Пароль"
                    v-model="password"
                    type="password"
                    outlined
                    class="ml-1"
                ></v-text-field>
            </v-row>

            <v-btn v-on:click="reg">
                Регистрация
            </v-btn>
        </v-card>
    </div>
</template>

<script>
export default {
  name: 'Registration',
  components: {
  },
  data() {
      return {
          password:'',
          login:'',
          name:'',
          email:'',
          company:'Unknown',
          photo:'https://upload.wikimedia.org/wikipedia/commons/9/99/Sample_User_Icon.png',
          city:'Unknown',
          website:'None'
      }
  },
  methods: {
    reg() {
      this.axios.get(`http://www.geoplugin.net/json.gp`)
      .then((response) => {
        this.city = response.data.geoplugin_city;
        let form_data = {
            "login": this.login,
            "password": this.password,
            "name": this.name,
            "website": this.website,
            "email": this.email,
            "city": this.city,
            "company": this.company,
            "photo": this.photo
        }
        this.axios.get(`http://37.77.104.246/api/jsonstorage/?id=e42c3957000fa1d66e09c8b7f48c08fa`)
        .then((response) => {
            response.data.push(form_data);
            this.axios.put(`http://37.77.104.246/api/jsonstorage/?id=e42c3957000fa1d66e09c8b7f48c08fa`, response.data)
            .then(() => {
                this.$emit('login', form_data);
                this.$router.push('/users/' + form_data.login);
            });
        });
      });
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
