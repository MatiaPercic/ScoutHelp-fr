<template>
  <div class="about">
    <h1>Registracija administratora</h1>

    <div class="container">
      <form>
        <p>
          *Lozinka novog administratora automatski je postavljena na admin1234
        </p>

        <div class="row justify-content-center">
          <div class="col-md-2">
            <input
              type="name"
              v-model="admin.ime"
              class="form-control"
              id="imputName"
              placeholder="Ime"
              required
            />
          </div>
          <div class="col-md-2">
            <input
              type="surname"
              v-model="admin.prezime"
              class="form-control"
              id="imputSurname"
              placeholder="Prezime"
              required
            />
          </div>
          <div class="col-md-1">
            <input
              type="godine"
              v-model="admin.godine"
              class="form-control"
              id="imputAgge"
              placeholder="Godine"
              required
            />
          </div>
        </div>
        <div class="row justify-content-center">
          <div class="col-md-4">
            <input
              type="email"
              v-model="admin.email"
              class="form-control"
              id="exampleInputEmail1"
              placeholder="email"
              required
            />
          </div>
        </div>

        <div class="row justify-content-center">
          <div class="col-md-4">
            <input
              type="pozicija"
              v-model="admin.pozicija"
              class="form-control"
              id="exampleInputPozicija"
              placeholder="Pozicija"
              required
            />
          </div>
        </div>

        <div class="d-grid gap-2 d-md-block">
          <button
            type="button"
            @click="buttonProfil()"
            class="btn btn-outline-primary"
          >
            Povratak na profil
          </button>

          <button
            type="submit"
            @click.prevent="register()"
            class="btn btn-primary"
          >
            Registriraj
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import router from "@/router";

export default {
  name: "registerAdmin",

  data() {
    return {
      admin: {
        ime: "",
        prezime: "",
        godine: "",
        email: "",
        pozicija: "",
      },
    };
  },
  async mounted() {},
  methods: {
    register() {
      if (
        !this.admin.ime ||
        !this.admin.prezime ||
        !this.admin.godine ||
        !this.admin.email ||
        !this.admin.pozicija
      )
        alert("Sva polja moraju biti upisana!");
      else {
        axios
          .post("https://scouthelp-f893.onrender.com/registerAdmin", this.admin)
          .then((response) => {
            console.log(response);
            if (response.data) {
              if (response.data == "Korisnik već postoji") {
                alert(
                  "Administrator a email adresom ",
                  this.admin.email,
                  " već postoji"
                );
              } else {
                alert(
                  "Uspiješna registracijaadministrator. Lozinka je postavljena kao 'admin123'"
                );
                console.log(response.data);
                console.log("uspijesan unos");

                this.$router.push({
                  name: "profilAdmin",
                });
              }
            }
          });
      }
    },

    buttonProfil(){
    this.$router.push({
      name: "profilAdmin"
    });
  }
  },
};

components: {
  router;
}
</script>

<style scoped>
h1 {
  margin-top: 30px;
}

.container {
  padding-left: 20px;
  padding-top: 25px;
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
  font-size: medium;
  opacity: 65%;
  color: #a020f0;
}
</style>
