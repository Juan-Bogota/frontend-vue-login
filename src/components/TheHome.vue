<template>
  <div>
    <nav class="navbar navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand">Navbar</a>
        <form class="d-flex">
          <button
            class="btn btn-outline-success"
            type="submit"
            @click.prevent="logoutUser()"
          >
            Search
          </button>
        </form>
      </div>
    </nav>
    <ul class="list-group">
      <li class="list-group-item active" aria-current="true">
        Name : {{ user.nombre }}
      </li>
      <li class="list-group-item">EMail: {{ user.email }}</li>
    </ul>
  </div>
</template>

<script>
import VueJwtDecode from "vue-jwt-decode";
export default {
  data() {
    return {
      user: {},
    };
  },
  methods: {
    logoutUser() {
      localStorage.removeItem("jwt");
      localStorage.removeItem("user");
      this.$router.push("/");
    },
    getUserData() {
      let token = localStorage.getItem("jwt");
      let user = localStorage.getItem("user");
      //let user = VueJwtDecode.decode(token);
      //console.log(user);
      this.user = JSON.parse(user); //localstorage necesita el parseo a objeto
      //this.user = user;
      console.log(this.user);
    },
  },
  created() {
    this.getUserData();
  },
};
</script>

<style scoped>
</style>