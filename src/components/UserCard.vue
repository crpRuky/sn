<template>
    <v-card
        class="pa-2 ma-5"
        max-width="1000"
        min-width="600"
        style="margin-bottom:50px"
        fluid
    >
        <v-row class="text-left">
            <v-col cols="4">
                <v-avatar size="160" class="ma-1">
                    <img :src="image" style="max-width: 100%">
                </v-avatar>
            </v-col>
            <v-divider vertical class="ma-5"></v-divider>
            <v-col class="text-left" max-width="400">
                <v-card-title>
                    <span class="headline font-weight-bold">{{username}}</span>
                </v-card-title>
                <v-card-text class="title font-weight-regular">
                    {{city}}
                </v-card-text>
                <v-card-actions>
                <v-btn outlined text color="success" link :to="'/users/' + id">
                    ПЕРЕЙТИ В ПРОФИЛЬ
                </v-btn>
                </v-card-actions>
            </v-col>
        </v-row>
    </v-card>
</template>

<script>
  export default {
    name: 'ProfileCard',
    props: {
        username:String,
        city:String,
        id:Number,
        image:String
    }
  }
</script>
