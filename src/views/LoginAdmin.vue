<template>
    <div class="about">
      <h2>Prijava administratora</h2>
  
      <p> 
        <router-link to="/"> Prijava volontera</router-link>
      </p>
       <div class="container">
        <form
          class="form-horizontal"
          @submit="login()"
          action="#"
          onsubmit="return false">
          <input
            type="email"
            v-model="loginCredentials.email"
            class="form-control"
            id="exampleInputEmail1"
            aria-describedby="emailHelp"
            placeholder="Unesi email"
          />
  
          <input
            type="password"
            v-model="loginCredentials.password"
            class="form-control"
            id="exampleInputPassword1"
            placeholder="Unesi lozinku"
          />
  
          <button type="submit" class="btn btn-primary">Submit</button>
        </form>
      </div> 
    </div>
  </template>
  
   <script>
  import axios from "axios";
  import ProfilVolonter from "./ProfilVolonter.vue";
  import router from "@/router";
  
  export default {
      name: "loginAdmin",
       created() {
          localStorage.clear();
      },
      async mounted() {},
      methods: {
          clearUser() {
              localStorage.removeItem("ime");
              localStorage.removeItem("prezime");
              localStorage.removeItem("godine");
              localStorage.removeItem("email");
              localStorage.removeItem("pozicija");
          },
          async setUser(user) {
              localStorage.setItem("ime", user.ime);
              localStorage.setItem("prezime", user.prezime);
              localStorage.setItem("godine", user.godine);
              localStorage.setItem("email", user.email);
              localStorage.setItem("pozicija", user.pozicija);
          },
          login() {
              axios
                  .post("http://localhost:3001/loginAdmin", this.loginCredentials)
                  .then((response) => {
                  console.log(response);
                  if (response.data) {
                      console.log(response.data);
                      this.clearUser();
                      this.setUser(response.data);
                      console.log(localStorage.getItem("ime"));
                      this.$router.replace({
                          name: "profilAdmin",
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
    }
  </script> 
  
  <style scoped>
  h2 {
    margin-top: 20px;
  }
  .container {
    width: 400px;
    padding-left: 20px;
    padding-top: 15px;
    display: block;
    margin-left: auto;
    margin-right: auto;
    
  }
  
  .form-control {
    text-align: justify;
    font-size: 17px;
    font-weight: unset;
    border-block-color: #a020f0;
    border-width: 1.5px;
    margin-bottom: 30px;
    margin-top: 30px;
  }
  
  button {
    margin: 1em;
    font-weight: bold;
    font-size: large;
    font-family: Arial;
    color: #a020f0;
    background-color: #fff;
    border-color: #a020f0;
    --bs-btn-hover-bg: #a020f0;
  }
  p{
    font-size: smaller;
    opacity: 50%;
    color: #a020f0;
  }
  </style>
  