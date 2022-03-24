<template>
  <div>
    <v-text-field
      v-model="username"
      label="UserName"
      hide-details="auto"
    ></v-text-field>
    <v-text-field v-model="password" label="PassWord"></v-text-field>
    <v-button @click="loginMethod">Login</v-button>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "App",
  data: () => ({
    username: "",
    password: "",
    token: "",
  }),
  methods: {
    loginMethod: async function () {
      try {
        const res = await axios.post(
          "https://file-managementt.herokuapp.com/authenticate",
          { username: this.username, password: this.password }
        );
        if (res !== null) {
          this.token = res.data.token;
          localStorage.setItem("token", this.token);
          console.log(res.data.token);
          this.$router.push("/");
        }
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
<style>
#app1 {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
