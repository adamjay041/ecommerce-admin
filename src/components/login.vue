<template>
<v-card
    class="mx-auto"
    max-width="344"
    outlined
>
    <v-card-title>
        <h3 class="text-center"> Login</h3>
    </v-card-title>
  <form>
    <v-text-field
      v-model="email"
      label="E-mail"
    >
    </v-text-field>
    <v-text-field
      v-model="password"
      label="Password"
      type="password"
    >
    </v-text-field>
    <v-btn class="mr-4" @click="login">submit</v-btn>
  </form>
</v-card>

</template>

<script>
import axios from 'axios'

export default {
  data: () => {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    login () {
      axios({
        url: 'http://localhost:3000/login',
        method: 'post',
        data: {
          email: this.email,
          password: this.password
        }
      })
        .then(data => {
          localStorage.setItem('token', data.data.token)
          this.$router.push('/')
        })
        .catch(err => {
          this.$store.commit('err', err)
        })
    }
  }
}
</script>

<style>

</style>
