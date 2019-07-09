<template>
  <v-container>
    <v-card class="pa-5">
      <v-text-field
        v-model="username"
        placeholder="Username"
      >
      </v-text-field>
      <v-text-field
        v-model="password"
        placeholder="Password"
        type="password"
      >
      </v-text-field>

      <v-btn block class="primary" @click="login">
        Login
      </v-btn>
    </v-card>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  name: 'Login',
  components: {},
  data () {
    return {
      username: 'asim',
      password: '123'
    }
  },
  methods: {
    login () {
      let data = {
        username: this.username,
        password: this.password
      }
      axios.post("/users/authenticate", data)
        .then((response) => {
            localStorage.setItem('user', JSON.stringify(response.data))
            this.$router.push("/")
        })
        .catch((errors) => {
            console.log("Cannot log in")
        })
    }
  }
}
</script>

<style>

</style>
