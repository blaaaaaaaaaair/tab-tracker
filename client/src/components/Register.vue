<template>
  <v-app>
    <v-flex pt-5 xs6 offset-xs3>
      <div class="white elevation-2">
        <v-toolbar dense color="light-blue darken-3" dark>
          <v-toolbar-title>Register</v-toolbar-title>
        </v-toolbar>
        <div class="pl-4 pr-4 pt-2 pb-2">
          <v-text-field 
            label="E-mail"
            v-model="email"
            required
          ></v-text-field>
          <v-text-field 
            label="Password"
            v-model="password"
            required
          ></v-text-field>
          <div class="form-error" v-html="error" />
          <br />
          <v-btn
            color="light-blue darken-3"
            dark
            @click="register">
            Register
          </v-btn>
        </div>
      </div>
    </v-flex>
  </v-app>
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
    async register () {
      try {
        await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
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
