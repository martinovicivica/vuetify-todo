<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-list class="pa-0" dense nav>
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
      color="blue accent-4"
      dense
      dark
      prominent
      :height="$route.path === '/' ? '220' : '170'"
    >
      <v-container class="pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>
        <v-row>
          <v-toolbar-title class="text-h4 ml-4">{{
            $store.state.appTitle
          }}</v-toolbar-title>
        </v-row>
        <v-row>
          <livedatetime />
        </v-row>
        <v-row v-if="$route.path === '/'">
          <field-add-task />
        </v-row>
      </v-container>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: false,
    items: [
      { title: "Todo", icon: "mdi-format-list-checks", to: "/" },

      { title: "About", icon: "mdi-help-box", to: "/about" },
    ],
  }),
  mounted() {
    this.$store.dispatch("getTasks");
  },
  components: {
    search: require("@/components/Tools/Search.vue").default,
    livedatetime: require("@/components/Tools/LiveDateTime.vue").default,
    "field-add-task": require("@/components/Todo/FieldAddTask.vue").default,
    snackbar: require("@/components/Shared/snackbar.vue").default,
  },
};
</script>
<style lang="sass">
.v-toolbar__content
  padding-left: 0px
</style>
