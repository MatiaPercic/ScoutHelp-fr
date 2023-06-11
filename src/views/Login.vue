<template>
  <div class="about">
    <h1>login page</h1>

    <div class="container">
      <form
        class="form-horizontal"
        @submit="login()"
        action="#"
        onsubmit="return false"
      >
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
  name: "login",

  created(){
    localStorage.clear();
  },
  async mounted() {},
  methods: {
    clearUser(){
      localStorage.removeItem('ime');
      localStorage.removeItem('prezime');
      localStorage.removeItem('godine');
      localStorage.removeItem('email');
      localStorage.removeItem('broj_aktivnosti');
      localStorage.removeItem('broj_volonterskih_sati');

    },

    async setUser(user){
      localStorage.setItem('ime',user.ime);
      localStorage.setItem('prezime',user.prezime);
      localStorage.setItem('godine',user.godine);
      localStorage.setItem('email',user.email);
      localStorage.setItem('broj_aktivnosti',user.broj_aktivnosti);
      localStorage.setItem('broj_volonterskih_sati',user.broj_volonterskih_sati);
    
    },

    login() {

      axios
        .post("http://localhost:3001/login", this.loginCredentials)

        .then((response) => {
          console.log(response);

          if (response.data) {
            console.log(response.data);
            this.clearUser();
            this.setUser(response.data);
            console.log(localStorage.getItem('ime'));
            this.$router.replace({
              name: "profilVolonter",
            });
          } else alert("Greška pri prijavljivanju, pokušajte ponovno!");
        });
    },
  },
  data() {
    return {

      loginCredentials: {
        email: "",
        password: "",
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
