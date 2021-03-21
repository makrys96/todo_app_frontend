<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-btn icon @click="redirectToHome()">
        <v-icon>mdi-home</v-icon>
      </v-btn>

      <v-spacer></v-spacer>

    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>


export default {
  name: 'App',
  methods: {
    redirectToHome() {
      this.$router.push({ path: '/' });
    },
  },
  components: {

  },

  data: () => ({
    //
  }),
};
</script>
