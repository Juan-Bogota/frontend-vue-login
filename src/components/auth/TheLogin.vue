<template>
  <form>
    <div class="mb-3">
      <label for="exampleInputEmail1" class="form-label">Email address</label>
      <input
        type="email"
        class="form-control"
        id="exampleInputEmail1"
        aria-describedby="emailHelp"
        v-model="login.email"
      />
      <div id="emailHelp" class="form-text">
        We'll never share your email with anyone else.
      </div>
    </div>
    <div class="mb-3">
      <label for="exampleInputPassword1" class="form-label">Password</label>
      <input
        type="password"
        class="form-control"
        id="exampleInputPassword1"
        v-model="login.password"
      />
    </div>
    <pre>
        {{ login }}
    </pre>

    <button type="submit" class="btn btn-primary" @click.prevent="loginUser()">
      Submit
    </button>
  </form>
</template>

<script>
import swal from "sweetalert";
export default {
  data() {
    return {
      login: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    async loginUser() {
      try {
        //console.log(this.login);
        let response = await this.$http.post("/api/usuario/login", this.login);
        console.log(response.data);
        let token = response.data.tokenReturn;
        let user = response.data.user;

        localStorage.setItem("jwt", token);
        localStorage.setItem("user", JSON.stringify(user));

        if (token) {
          swal("Login Correct", "Los datos estan ok", "success");
          this.$router.push("/home");
        }
      } catch (e) {
        swal("Login Incorrrect", "Datos erroneos", "error");
        console.log(e);
      }
    },
  },
};
</script>

<style scoped>
</style>