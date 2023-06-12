<template>
  <h3>Profil admina</h3>
</template>

<script>
export default {
  name: "profilAdmin",
};
</script>
<template>
  <div class="about">
    <h3 class="row">
      <div class="row justify-content-between">
        <div class="col-4">Osobni podaci:</div>
        <div class="col-4" style="text-align: center">Izbornik:</div>
      </div>
    </h3>

    <div class="row justify-content-between">
      <div class="col-4">
        <p class="plain">
          <br />
          Ime i Prezime: {{ admin.ime }} {{ admin.prezime }}
          <br />
          <br />
          Goidine: {{ admin.godine }}
          <br />
          <br />
          pozicija: {{ admin.pozicija }}
          <br />
          <br />
        </p>

        <p class="sub_text">Izmjena osobnih podataka</p>
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
  margin-top: 25px;
  margin-left: 10%;
  margin-top: 1%;
}

h3 {
  margin-top: 3%;
  text-align: left;
  margin-left: 3%;
  margin-top: 3%;
  color: #a020f0;
}

.sub_text {
  text-align: left;
  margin-top: 45px;
  margin-left: 4%;
  font-size: smaller;
  text-decoration: underline;
  font-style: oblique;
  opacity: 40%;
  color: #a020f0;
}

.ogranicenje {
  text-align: center;
  font-size: 12px;
  opacity: 60%;
  color: #a020f0;
}
</style>
