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

      <div class="col-4">
        <button
          type="button"
          class="btn btn-primary"
          style="
            margin: 4em;
            font-weight: bold;
            font-family: Arial;
            color: #a020f0;
            background-color: #fff;
            border-color: #a020f0;
          "
        >
          <router-link
            style="
              font-size: 15px;
              color: #a020f0
              text-decoration: none; "
            to="/aktivnostiadmin"
            >Prikaz volonterskih aktivnosti</router-link
          >
        </button>
      </div>
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
      },
    };
  },

  mounted() {
    this.info();
  },

  methods: {
    info() {
      this.admin.ime = localStorage.getItem("ime");
      this.admin.prezime = localStorage.getItem("prezime");
      this.admin.godine = localStorage.getItem("godine");
      this.admin.pozicija = localStorage.getItem("pozicija");
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
  margin-top: 65px;
}
.sub_text {
  font-size: medium;
  text-decoration: underline;
  font-style: oblique;
  opacity: 65%;
  color: #a020f0;
}
</style>
