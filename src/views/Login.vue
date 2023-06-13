<template>
  <div class="about">
    <h1>Prijava volontera</h1>

    <p > 
      <router-link to="/loginAdmin" class="custom-text"> Prijava administratora</router-link>
    </p>
    <div class="container">
      <form>
        <div class="row justify-content-center">
            <div class="col-md-5">
        <input
          type="email"
          v-model="loginCredentials.email"
          class="form-control"
          id="exampleInputEmail1"
          aria-describedby="emailHelp"
          placeholder="Unesi email"
        />
        </div>
      </div>
        <div class="row justify-content-center">
          <div class="col-md-5">
        <input
          type="password"
          v-model="loginCredentials.password"
          class="form-control"
          id="exampleInputPassword1"
          placeholder="Unesi lozinku"
        />
        </div>
      </div>
        <button type="submit" @click.prevent="login()"
        class="btn btn-primary">Submit</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import router from "@/router";

export default {
    name: "login",
    created() {
        localStorage.clear();
    },
    async mounted() {
        let dataCheck = localStorage.getItem("broj_aktivnosti");
        if (dataCheck) {
            this.$router.push({ name: "profilVolonter" });
        }
    },
    methods: {
        clearUser() {
            localStorage.removeItem("ime");
            localStorage.removeItem("prezime");
            localStorage.removeItem("godine");
            localStorage.removeItem("email");
            localStorage.removeItem("broj_aktivnosti");
            localStorage.removeItem("broj_volonterskih_sati");
        },
        async setUser(user) {
            localStorage.setItem("ime", user.ime);
            localStorage.setItem("prezime", user.prezime);
            localStorage.setItem("godine", user.godine);
            localStorage.setItem("email", user.email);
            localStorage.setItem("broj_aktivnosti", user.broj_aktivnosti);
            localStorage.setItem("broj_volonterskih_sati", user.broj_volonterskih_sati);
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
                    console.log(localStorage.getItem("ime"));
                    this.$router.replace({
                        name: "profilVolonter",
                    });
                }
                else
                    alert("Greška pri prijavljivanju, pokušajte ponovno!");
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
    components: { router }
};
</script>

<style scoped>
h1 {
  margin-top: 30px;
}
.container {
  padding-left: 20px;
  padding-top: 12px;
  display: block;
  margin-left: auto;
  margin-right: auto;
  
}

.form-control {
  text-align: justify;
  font-size: 18px;
  opacity: 65%;
  border-block-color: #a020f0;
  border-width: 2px;
  margin-bottom: 20px;
  margin-top: 30px;
}

button {
  margin-top: 30px;
  font-weight: bold;
  font-size: larger;
  font-family: Arial;
  color: #a020f0;
  background-color: #fff;
  border-color: #a020f0;
  --bs-btn-hover-bg: #a020f0;
}
.custom-text{
  font-size: medium;
 opacity: 65%;
  color: #a020f0;
}
</style>
