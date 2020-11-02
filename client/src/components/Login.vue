<template>
  <v-flex xs6 offset-xs3>
    <div class="white elevation-2">
      <v-toolbar dense color="light-blue darken-3" dark>
        <v-toolbar-title>Login</v-toolbar-title>
      </v-toolbar>
      <div class="pl-4 pr-4 pt-2 pb-2">
        <v-text-field 
          label="E-mail"
          v-model="email"
          required
        ></v-text-field>
        <v-text-field 
          label="Password"
          type="password"
          v-model="password"
          required
        ></v-text-field>
        <div class="form-error" v-html="error" />
        <br />
        <v-btn
          color="light-blue darken-3"
          dark
          @click="login">
          Login
        </v-btn>
      </div>
    </div>
  </v-flex>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async login () {
      try {
        const response = await AuthenticationService.login({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  },
}
</script>

<style scoped>
  .form-error {
    color: red;
  }
</style>
