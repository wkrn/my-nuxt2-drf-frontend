<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      app
      right
    >
      <v-list dense>
        <v-list-item class="px-2">
          <v-list-item-avatar>
            <!-- <v-img v-if="user.avatar_url" :src="user.avatar_url"></v-img>
            <v-icon v-else>face</v-icon> -->
          </v-list-item-avatar>

          <v-list-item-title>John Leider</v-list-item-title>

          <v-btn
            icon
            @click.stop="">
            <v-icon>mdi-chevron-left</v-icon>
          </v-btn>
        </v-list-item>
        <v-list-item
            v-for="route in routes"
            :key="route.name"
            :to="route.to"
            exact>
          <v-list-item-icon>
            <v-icon>{{ route.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ route.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="cyan"
      dark
    >
      <v-spacer></v-spacer>

      <v-toolbar-title>Application</v-toolbar-title>

      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
    </v-app-bar>

    <v-main>
      <v-container
        class="fill-height"
        fluid
      >
        <v-row
          align="center"
          justify="center"
        >
          <v-col class="text-center">
            <v-tooltip left>
              <template v-slot:activator="{ on }">
                <v-btn
                  :href="source"
                  icon
                  large
                  target="_blank"
                  v-on="on"
                >
                  <v-icon large>mdi-code-tags</v-icon>
                </v-btn>
              </template>

              <span>Source</span>
            </v-tooltip>
          </v-col>
        </v-row>
      </v-container>
    </v-main>

    <v-footer
      color="cyan"
      app
    >
      <v-spacer></v-spacer>

      <span class="white--text">&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
    name: 'LayoutsDemosBaselineFlipped',
    props: {
      source: String,
    },
    data: () => ({
      drawer: null,
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        },
        { title: 'Home', icon: 'mdi-home-city' },
        { title: 'My Account', icon: 'mdi-account' },
        { title: 'Users', icon: 'mdi-account-group-outline' },
      ],
      allRoutes: [
        { to: { name: 'index' }, title: 'home', icon: 'mdi-home', exact: true },
        { to: { name: 'users' }, title: 'users', icon: 'mdi-account-group', exact: true, permission: false },
        { to: { name: 'settings' }, title: 'settings', icon: 'mdi-settings' },
        { to: { name: 'auth-login' }, title: 'login', icon: 'mdi-fingerprint', permission: true },
        { to: { name: 'auth-registration' }, title: 'registration', icon: 'mdi-account-plus', permission: true },
        { to: { name: 'auth-logout' }, title: 'logout', icon: 'mdi-logout', permission: false },
      ],
      userDropdownRoutes: [
        { to: { name: 'auth-user-edit' }, title: 'user-edit', icon: 'edit' },
        { to: { name: 'auth-password-change' }, title: 'password-change', icon: 'security' },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }),
    computed: {
      ...mapGetters({ user: 'auth/user', loggedIn: 'auth/loggedIn' }),
      settings() {
        return this.$store.state.settings;
      },
      routes() {
        return this.allRoutes.filter(({ permission }) => permission !== this.loggedIn);
      }
    },
    methods: {
      // changeSingleSetting(key) {
      //   this.$store.commit('settings/CHANGE_SETTING', key);
      //   this.$store.dispatch('settings/saveSettings');
      // }
    },
    mounted() {
      // this.$store.dispatch('settings/loadSettings');
    }
  }
</script>
