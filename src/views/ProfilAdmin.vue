<template>
  <div class="about">
    <h1 class="row">
      <div class="row justify-content-between">
        <div class="col-4">Osobni podaci:</div>
        <div class="col-4" style="text-align: center">Izbornik:</div>
      </div>
    </h1>

    <div class="row justify-content-between">
      <div class="col-5">
        <p class="plain">
          <br />
          Ime i Prezime: {{ admin.ime }} {{ admin.prezime }}
          <br />
          <br />
          Godine: {{ admin.godine }}
          <br />
          <br />
          Pozicija: {{ admin.pozicija }}
          <br />
          <br />
        </p>

        <p class="align">
          <router-link to="/updateAdmin" class="sub_text">
            Izmijena osobnih podataka</router-link
          >
        </p>
      </div>

      <div class="col-4 ">
        <button type="button" @click="buttonAktivnosti()" class="btn btn-outline-secondary">

            Prikaz volonterskih aktivnosti
          
        </button>

        <button type="button" @click="buttonRegister()" class="btn btn-outline-secondary">

            Registracija novog administratora

        </button>
      </div>
    </div>

    <div>
      <b-alert show variant="warning" v-if="showWarn">
        <router-link to="/updateAdmin" class="alert-link"
          >Lozinka postavljena na 'admin1234' pri registraciji. Promijenite ju
          radi osobne sigurnosti!</router-link
        >
      </b-alert>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "profilAdmin",

  data() {
    return {
      admin: {
        ime: "",
        prezime: "",
        godine: null,
        pozicija: "",
        password: "",
      },
      showWarn: false,
    };
  },

  mounted() {
    this.info();
    this.passwordWarn();
  },

  methods: {
    info() {
      this.admin.ime = localStorage.getItem("ime");
      this.admin.prezime = localStorage.getItem("prezime");
      this.admin.godine = localStorage.getItem("godine");
      this.admin.pozicija = localStorage.getItem("pozicija");
      this.admin.password = localStorage.getItem("password");
    },
    passwordWarn() {
      if (this.admin.password == "admin1234") this.showWarn = true;
    },
    buttonRegister(){
      this.$router.push({
        name:"registerAdmin"
      });
    },
    buttonAktivnosti(){
      this.$router.push({
        name:"aktivnosti"
      });
    },
  

  },
};
</script>

<style scoped>
.plain {
  text-align: left;
  margin-top: 20px;
  margin-left: 10%;
  font-size: 25px;
}

h1 {
  text-align: left;
  margin-left: 3%;
  margin-top: 50px;
  color: #a020f0;
}

.align {
  text-align: left;
  margin-left: 10%;
  margin-top: 30px;
  margin-bottom: 20px;
}
.sub_text {
  font-size: medium;
  text-decoration: underline;
  font-style: oblique;
  opacity: 65%;
  color: #a020f0;
}

button {
  margin-top: 30px;
  font-weight: bold;
  font-size: larger;
  font-family: Arial;
  color: #a020f0;
  background-color: #fff;
  border-color: #a020f0;

}
 button:hover{
  background-color: #a020f0;
  color: #fff;
}

b-alert {
  margin-top: 20px;
}
</style>
