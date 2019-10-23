<template>
  <v-app>
    <v-app-bar color=" error" dark app>
      <v-toolbar-title class="headline">
        <span>HeadsUp</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn text @click="logout">
        <span class="mr-2">Logout</span>
      </v-btn>
    </v-app-bar>

    <v-content>
      <router-view />
    </v-content>
  </v-app>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    //
  }),
  computed: {
    user() {
      return;
    }
  },
  methods: {
    logout() {
      localStorage.clear();
      this.$router.push({ name: "home", to: "/" });
    }
  }
};
</script>
