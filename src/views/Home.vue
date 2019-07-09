<template>
	<v-layout>
		<h2>Dashboard</h2>
		<p>Name: {{ user.name }}</p>

		<!-- <input type="file" accept="image/*" capture="camera" /> -->
	</v-layout>
</template>

<script>
import axios from "axios"
import router from "../router"
export default {
  name: "Login",
  data() {
    return {
      user: {
        name: "Jesse"
      }
    }
  },
  methods: {
    getUserData: function() {
      let self = this
      let token = JSON.parse(localStorage.getItem('user')).token

      let config = {
        headers: {
          Authorization: "Bearer " + token
        }
      }

      debugger
      axios.get("/users", config)
      .then((response) => {
        console.log(response)
        // self.$set(this.user, name , response.data[1].firstName)
        this.user.name = response.data[1].firstName
      })
      .catch((errors) => {
        console.log(errors)
        router.push("/")
      })
    }
  },
  mounted() {
    this.getUserData()
  }
}
</script>
