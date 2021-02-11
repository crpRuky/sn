<template>
        <v-card
          class="mx-auto"
          max-width="1000"
          style="margin-bottom:50px"
        >
          <v-card-title>
            <span class="headline font-weight-bold"><slot name="title"></slot></span>
          </v-card-title>

          <v-card-text class="title font-weight-regular">
            <slot></slot>
          </v-card-text>

          <v-card-actions>
            <v-list-item class="grow">
              <v-list-item-avatar>
                <v-img
                  class="elevation-6"
                  alt=""
                  :src="image"
                ></v-img>
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title>{{author}}</v-list-item-title>
              </v-list-item-content>

              <v-row
                align="center"
                justify="end"
              >
                <v-icon class="mr-1">
                  mdi-heart
                </v-icon>
                <span class="subheading mr-2">{{likes}}</span>
              </v-row>
            </v-list-item>
          </v-card-actions>
        </v-card>
</template>

<script>
  export default {
    name: 'ProfileCard',
    props: {
        author:String,
        likes:Number,
        image:String
    }
  }
</script>
