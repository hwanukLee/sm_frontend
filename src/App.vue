<template>
  <v-app
    style="background: #FAFAF0;"
  >
    <v-navigation-drawer 
      app
      v-model="drawer"
      absolute
      temporary
    >
      <v-list
        nav
        dense
      >
        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >
          <v-list-item to="/">
            <v-list-item-icon>
              <v-icon>fa-home</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item>
          <v-list-item to="/prices">
            <v-list-item-icon>
              <v-icon>fa-list</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Prices</v-list-item-title>
          </v-list-item>

          <v-spacer></v-spacer>

          <v-list-item to="/account">
            <v-list-item-icon>
              <v-icon>fa-user</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Acount</v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      flat
      :prominent="prominent"
      :color="bg_color"
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-app-bar-title
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          width="100"
        >
          Space Marine
        </v-app-bar-title>
      </div>

      <v-spacer></v-spacer>

      <div 
        class="d-flex align-right"
      >
        <div
          class="shrink mt-1 hidden-sm-and-down"
        >
          <v-tabs
            align-with-title
            :background-color="bg_color"
          >
            <v-tab to="/">
              Home
            </v-tab>
            <v-tab to="/prices">
              Prices
            </v-tab>
            <v-tab to="/account">
              Account
            </v-tab>
            <v-tabs-slider color="black"></v-tabs-slider>
          </v-tabs>

        </div>
        <v-app-bar-nav-icon 
          class="shrink mt-1 hidden-md-and-up"
          @click="drawer = true"></v-app-bar-nav-icon>
      </div>
    </v-app-bar>

    <!-- Sizes your content based upon application components -->
    <v-main>

      <!-- Provides the application the proper gutter -->
      <v-container fluid>

        <!-- If using vue-router -->
        <router-view></router-view>

        <v-fab-transition>
          <v-btn
            color="indigo"
            dark
            fixed
            bottom
            right
            fab
            @click="$vuetify.goTo(target, options)"
          >
            <v-icon>mdi-chevron-up</v-icon>
          </v-btn>
        </v-fab-transition>
      </v-container>
    </v-main>

    <v-footer app>
      <v-row
        align="center"
        justify="center"
      >
        <v-col
          class="text-center"
          cols="12"
        >
          Copyrightⓒ2021 All rights reserved Space-Marine Co.
        </v-col>
      </v-row>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'App',

  data: () => ({
    drawer: false,
    prominent: false,
    bg_color: '#FAFAF0',
    type: 'number',
    number: 0,
    duration: 500,
    offset: 0,
    easing: 'easeInOutCubic',
  }),

  computed: {
    target() {
      return Number(this[this.type])
    },
    options() {
      return {
        duration: this.duration,
        offset: this.offset,
        easing: this.easing
      }
    }
  }
};
</script>