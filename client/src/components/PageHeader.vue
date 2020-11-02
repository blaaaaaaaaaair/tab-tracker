<template>
  <v-app-bar
    app
    fixed
    dark
    color="light-blue darken-3">
    <v-toolbar-title
      class="mr-4 home"
      @click="navigateTo({name: 'home'})">
      TabTracker
    </v-toolbar-title>
    <v-btn text>Browse</v-btn>
    <v-spacer></v-spacer>

    <v-btn
      text
      @click="navigateTo({name: 'login'})"
      v-if="!$store.state.isUserLoggedIn">
      Login
    </v-btn>

    <v-btn
      text
      @click="navigateTo({name: 'register'})"
      v-if="!$store.state.isUserLoggedIn">
      Sign Up
    </v-btn>
  </v-app-bar>
</template>

<script>
export default {
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    }
  }
}
</script>

<style scoped>
  .home {
    cursor: pointer;
  }
</style>
