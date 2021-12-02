<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" :mobile-breakpoint="768" app>
      <v-img
        class="pa-4 pt-7"
        lazy-src="../public/images/todo-menu-images.jpg"
        src="../public/images/todo-menu-images.jpg"
        height="170"
        gradient="to top right, rgba(55,236,236,.2), rgba(25,32,72,.8)"
      >
        <v-avatar size="70" class="mb-2">
          <img src="https://cdn.vuetifyjs.com/images/john.jpg" alt="John" />
        </v-avatar>
        <div class="text-shadox white--text text-subtitle-1 font-weight-bold">
          User name
        </div>
        <div class="text-shadox white--text text-subtitle-2">user__name</div>
      </v-img>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="primary"
      dark
      lazy-src="../public/images/banner.jpg"
      prominent
      height="170"
      src="../public/images/banner.jpg"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(55,236,186,.1), rgba(25,32,72,.5)"
        ></v-img>
      </template>
      <v-container class="header-container pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>
        <v-row>
          <v-toolbar-title class="text-shadox text-h4 ml-4">{{
            $store.state.appTitle
          }}</v-toolbar-title>
        </v-row>
        <live-date-time class="text-shadox" />
      </v-container>
    </v-app-bar>
    <v-sheet id="scrolling-techniques-5" max-height="600"> </v-sheet>
    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
import Search from "@/components/Tools/Search";
import LiveDateTime from "@/components/Tools/LiveDateTime";
import SnackBar from "@/components/Shared/Snackbar";
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: "Todo", icon: "mdi-format-list-checks", to: "/" },
      { title: "About", icon: "mdi-help-box", to: "/about" },
    ],
  }),
  mounted() {
    this.$store.dispatch("getTasks");
  },
  // computed: {
  //   appTitle() {
  //     return process.env.VUE_APP_TITLE;
  //   },
  // },
  components: {
    snackbar: SnackBar,
    search: Search,
    "live-date-time": LiveDateTime,
  },
};
</script>

<style lang="sass">
.header-container
  max-width: none !important

.text-shadox
  text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black
</style>
