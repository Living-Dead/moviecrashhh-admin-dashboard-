<template>
  <v-menu
    :close-on-content-click="false"
    bottom
    left
    min-width="300"
    max-width="300"
    nudge-left="12"
    offset-x
    transition="slide-y-transition"
    dark
  >
    <template v-slot:activator="{ on }">
      <v-btn
        v-on="on"
        class="elevation-0"
        color="grey"
        dark
        fab
        fixed
        style="top: 50%;"
        top
      >
        <v-icon>mdi-settings</v-icon>
      </v-btn>
    </template>
    <v-card>
      <v-container grid-list-xl>
        <v-layout wrap>
          <v-flex xs12>
            <div class="text-xs-center body-2 text-uppercase ">Sidebar Filters</div>

            <v-layout justify-center>
              <v-avatar
                v-for="c in colors"
                :key="c"
                :class="[c === color ? 'color-active ' + c: c]"
                size="23"

                @click="setColor(c)"
              />
            </v-layout>
            <v-divider class="mt-3"/>
          </v-flex>
          <v-flex
            xs12
          >
            <div class="text-xs-center body-2 text-uppercase ">Images</div>
          </v-flex>
          <v-flex
            v-for="img in images"
            :key="img"
            xs3
          >
            <v-img
              :class="[image === img ? 'image-active' : '']"
              :src="img"
              height="120"
              @click.native="setImage(img)"
            />
          </v-flex>
          <v-flex xs12>
            <v-btn
              href="https://github.com/ClintOxx/vuetify-admin-dashboard"
              target="_blank"
              class="white--text"
              :color="color"
              block
            >
              Documentation
            </v-btn>
          </v-flex>
        </v-layout>
      </v-container>
    </v-card>
  </v-menu>
</template>

<script>
// Utilities
import {
  mapMutations,
  mapState
} from 'vuex'

export default {
  data: () => ({
    colors: [
      'primary',
      'success',
      'warning',
      'red',
    ],
    images: [
      'https://demos.creative-tim.com/vue-material-dashboard/img/sidebar-2.32103624.jpg',
      'https://demos.creative-tim.com/vue-material-dashboard/img/sidebar-3.3a54f533.jpg',
      'https://demos.creative-tim.com/vue-material-dashboard/img/sidebar-4.3b7e38ed.jpg',
      ''
    ]
  }),

  computed: {
    ...mapState('app', ['image', 'color']),
    color () {
      return this.$store.state.app.color
    }
  },

  methods: {
    ...mapMutations('app', ['setImage']),
    setColor (color) {
      this.$store.state.app.color = color
    }
  }
}
</script>

<style lang="scss">
  .v-avatar,
  .v-responsive {
    cursor: pointer;
  }
</style>
