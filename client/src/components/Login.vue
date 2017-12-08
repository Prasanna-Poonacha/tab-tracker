<template>
  <v-layout column>
    <v-flex xs6 offset-xs3>
      <div class="white elevation-2">
        <v-toolbar flat dense class="cyan" dark>
          <v-toolbar-title>Login</v-toolbar-title>
        </v-toolbar>
        <div class="pl-4 pr-4 pt-2 pb-2">
          <v-text-field
              type="email"
              v-model="email"
              label="Email"
            ></v-text-field>          
            <br>
            <v-text-field
              type="password"
              v-model="password"
              label="Password"
            ></v-text-field>          
            <br>
            <div class="error" v-html="error"></div>
            <br>
          <v-btn class="cyan"
            @click="register" dark>Login</v-btn>
          </div>
      </div>
    </v-flex>
  </v-layout>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: 'example@mail.com',
      password: '',
      error: null
    }
  },
  methods: {
    async register () {
      try {
        await AuthenticationService.login({
          email: this.email,
          password: this.password
        })
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  },
  watch: {
    email (value) {
      console.log('email has changed: ' + value)
    }
  },
  mounted () {
    console.log('mounted')
  }
}
</script>

<style scoped>
  .error{
    color: red;
  }
</style>
