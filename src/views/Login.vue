<template>
  <div class="about">
    <h1>login page</h1>

    <div class="container">
      <form class="form-horizontal" @submit="checkCredentials()" action="#" onsubmit="return false">
        <div class="form-group">
          <label for="exampleInputEmail1" class="plain">Email address</label>

          <div class="col-sm-10">
            <input
              type="email"
              v-model="loginCredentials.email"
              class="form-control"
              id="exampleInputEmail1"
              aria-describedby="emailHelp"
              placeholder="Enter email"
            />
          </div>
        </div>

        <div class="form-group">
          <label for="exampleInputPassword1" class="plain">Password</label>

          <div class="col-sm-10">
            <input
              type="password"
              v-model="loginCredentials.password"
              class="form-control"
              id="exampleInputPassword1"
              placeholder="Password"
            />
          </div>
        </div>

        <div class="row"></div>

        <div class="form-group">
          <div class="col-sm-offset-2 col-sm-10">
            <button
              type="submit"
              class="btn btn-primary"
              style="
                margin: 2em;
                font-weight: bold;
                font-size: large;
                font-family: Arial;
                color: #a020f0;
                background-color: #fff;
                border-color: #a020f0;
              "
            >
              Submit
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>

</template>

<script>

import axios from "axios";


export default {
  name: 'login',

  async mounted() {},
  methods: {
    checkCredentials() {
      axios
        .post("http://localhost:3001/login", this.loginCredentials)
        .then(console.log("yes"))
        .then((response) => {
          this.$router.push({
            name: "profil",
          });
        });
    },
  },
  data() {
    return {
      adminLogin: 0,
      loginCredentials: {
        email: "mpercic@gmail.com",
        password: "percic",
      },
    };
  },
    
};

</script>

<style scoped>
.plain {
  text-align: justify;
  font-size: 20px;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: bold;
  row-gap: 5;
}

.form-control {
  text-align: justify;
  font-size: 20px;
  font-weight: unset;
  border-block-color: #a020f0;
}
</style>