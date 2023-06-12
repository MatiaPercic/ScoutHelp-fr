<template>
  <div class="about">
    <h1>Registracija volontera</h1>

    <div class="container">
      <form>
        <div class="row justify-content-center">
          <div class="col-md-2">
            <input
              type="name"
              v-model="reg.ime"
              class="form-control"
              id="imputName"
              placeholder="Ime"
              required
            />
          </div>
          <div class="col-md-2">
            <input
              type="surname"
              v-model="reg.prezime"
              class="form-control"
              id="imputSurname"
              placeholder="Prezime"
              required
            />
          </div>
          <div class="col-md-1">
            <input
              type="godine"
              v-model="reg.godine"
              class="form-control"
              id="imputAgge"
              placeholder="Godine"
              required
            />
          </div>
        </div>
        <div class="row justify-content-center">
          <div class="col-md-5">
            <input
              type="email"
              v-model="reg.email"
              class="form-control"
              id="exampleInputEmail1"
              placeholder="Enter email"
              required
            />
          </div>
        </div>

        <div class="row justify-content-center">
          <div class="col-md-3 custom">
            <input
              type="password"
              v-model="reg.password"
              class="form-control"
              id="exampleInputPassword1"
              placeholder="Password"
              required
            />
          </div>
          <div class="col-md-3 custom">
            <input
              type="password"
              v-model="reg.repass"
              class="form-control"
              id="exampleInputPassword2"
              placeholder="Repeat password"
              required
            />
          </div>
        </div>

        <button
          type="submit"
          @click.prevent="register()"
          class="btn btn-primary"
        >
          Submit
        </button>

        
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ProfilVolonter from "./ProfilVolonter.vue";
import router from "@/router";

export default {
  name: "register",
  created() {
    localStorage.clear();
  },
  data() {
    return {
      reg: {
        ime: "",
        prezime: "",
        godine: null,
        email: "",
        password: "",
        repass: "",
      },
    };
  },
  async mounted() {},
  methods: {
    register() {
      if (
        !this.reg.ime ||
        !this.reg.prezime ||
        !this.reg.godine ||
        !this.reg.email ||
        !this.reg.password ||
        !this.reg.repass
      )
        alert("Sva polja moraju biti upisana!");
      else {
        if (this.reg.password != this.reg.repass) {
          alert("Lozinka mora biti jednaka u oba polja");
          return;
        } else {
          axios
            .post("http://localhost:3001/register", this.reg)
            .then((response) => {
              console.log(response);
              if (response.data) {
                if(response.data=="Korisnik već postoji"){
                    alert("korisnik već postoji");
                }
                else{
                alert("Uspiješna registracija");
                console.log(response.data);
                console.log("uspijesan unos");

                this.$router.push({
                  name: "login",
                });
            }
              }
            });
        }
      }
    },
  },

  components: { router },
};
</script>

<style scoped>
h1 {
  margin-top: 30px;
}

.container {
  padding-left: 20px;
  padding-top: 50px;
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
.custom {
  width: 270px;
}
button {
  /*   margin: 1em; */
  margin-top: 30px;
  font-weight: bold;
  font-size: larger;
  font-family: Arial;
  color: #a020f0;
  background-color: #fff;
  border-color: #a020f0;
  --bs-btn-hover-bg: #a020f0;
}
p {
  font-size: smaller;
  opacity: 60%;
  color: #a020f0;
}
</style>
