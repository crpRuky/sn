<template>
    <v-container align="center" justify="center">
        <v-row class="text-left">
            <v-col cols="10">
                <h1 class="green--text text--darken-2">
                    <v-icon large color="green darken-2">mdi-account-outline</v-icon>
                    Иван Иванов
                </h1>
            </v-col>
        </v-row>
        <v-row class="text-left">
            <v-col cols="2">
                <img src="https://randomuser.me/api/portraits/men/7.jpg" style="max-width: 100%">
            </v-col>
            <v-col cols="10" class="text-left" max-width="400">
                <p>
                    Веб-сайт: <a href="https://example.com" target="_blank">example.com</a>
                </p>
                <p>
                    E-mail: <a href="mailto:...">example@email.com</a>
                </p>
                <p>
                    Город: Москва
                </p>
                <p>
                    Место работы: Нет
                </p>
            </v-col>
        </v-row>

        <v-divider style="margin:30px 0px 30px 0px"></v-divider>

        <profile-card :author="'Иван'" :likes="256" :shares="64">
          <template v-slot:title>Title</template>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolores incidunt placeat explicabo atque numquam. Illo expedita a, aliquid laboriosam ipsam aut, esse dignissimos deserunt unde alias ad nobis?
        </profile-card>

        <hr style="background-color:transparent; border:none; height:50px">

        <profile-card :author="'Иван'" :likes="320" :shares="54">
          <template v-slot:title>Title</template>
          Lorem ipsum, dolor sit amet consectetur adipisicing elit. Voluptatum dignissimos aperiam voluptate provident dolore iusto esse rerum rem soluta! Recusandae doloribus, magnam sit maxime eveniet laudantium accusantium ducimus esse impedit.
        </profile-card>

    </v-container>
</template>

<script>
import ProfileCard from '../components/ProfileCard.vue'

export default {
  name: 'Profile',
  components: {
    ProfileCard
  }
}
</script>
