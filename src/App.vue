<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" :mobile-breakpoint="768" app>
      <v-img
        class="pa-4 pt-7"
        gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        height="170"
        src="mountains.jpg"
      >
        <v-avatar size="70" class="mb-2">
          <img src="555.jpg" alt="555" />
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">
          Oleg Maris
        </div>
        <div class="white--text text-subtitle-2">o_maris</div>
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
      :height="$route.path === '/' ? '225' : '170'"
      color="primary"
      src="mountains.jpg"
      app
      dark
      prominent
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.7), rgba(128,208,199,.9)"
        ></v-img>
      </template>

      <v-container class="header-container pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer" />
          <v-spacer></v-spacer>
          <search />
        </v-row>

        <v-row>
          <v-app-bar-title class="text-h4 ml-4">
            {{ $store.state.appTitle }}
          </v-app-bar-title>
        </v-row>

        <v-row>
          <live-date-time />
        </v-row>

        <v-row v-if="$route.path === '/'">
          <field-add-task />
        </v-row>
      </v-container>
    </v-app-bar>

    <v-main>
      <router-view />
      <snack-bar />
    </v-main>
  </v-app>
</template>

<script>
export default {
  components: {
    search: require("@/components/tools/Search.vue").default,
    "live-date-time": require("@/components/tools/LiveDateTime.vue").default,
    "snack-bar": require("@/components/shared/SnackBar.vue").default,
    "field-add-task": require("@/components/todo/FieldAddTask.vue").default,
  },
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
};
</script>

<style lang="sass">
.header-container
  max-width: none !important
</style>
