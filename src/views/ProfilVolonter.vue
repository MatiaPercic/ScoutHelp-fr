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
          Ime i Prezime: {{ volonter.ime }} {{ volonter.prezime }}
          <br />
          <br />
          Goidine: {{ volonter.godine }}
          <br />
          <br />
          Broj volonterskih aktivnosti: {{ volonter.broj_aktivnosti }}
          <br />
          <br />
          Broj odrađenih volonterskih sati:
          {{ volonter.broj_volonterskih_sati }}
          <br />
        </p>
    
      <p class="sub_text">Izmjena lozinke ili email-a</p>
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
        to="/aktivnostiVolonter"
        >Prikaz volonterskih aktivnosti</router-link
      >
    </button>

    <p class="ogranicenje">
      *Volonterima nije omogućeno mijenjanje
      <br />
      niti unos novih podataka vezanih za  
      <br />
      volonterske aktivnosti. U slučaju 
      <br/>
      primjećivanja krivih podataka, obratite se
      <br/> 
      osobi s administrativnom ulogom
    </p>
  </div>
</div>
</div>
</template>

<script>
import axios from "axios";


export default {
  // name: "profilVolonter",


  data() {
    return {
      volonter: {
        ime: "",
        prezime: "",
        godine: null,
        broj_aktivnosti: null,
        broj_volonterskih_sati: null,
      },
    };
  },

  mounted() {
    this.info();
  },

  methods: {
    info() {
      this.volonter.ime = localStorage.getItem("ime");
      this.volonter.prezime = localStorage.getItem("prezime");
      this.volonter.godine = localStorage.getItem("godine");
      this.volonter.broj_aktivnosti = localStorage.getItem("broj_aktivnosti");
      this.volonter.broj_volonterskih_sati = localStorage.getItem("broj_volonterskih_sati");
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
