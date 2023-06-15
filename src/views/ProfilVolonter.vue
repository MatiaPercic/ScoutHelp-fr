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
    
      <p class="align">
        <router-link to="/updateVolonter" class="sub_text"> Izmijena osobnih podataka</router-link>
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
        to="/aktivnostiVolonter"
        >Prikaz volonterskih aktivnosti</router-link
      >
    </button>

    <p class="ogranicenje">
      *Volonterima nije omogućeno mijenjanje niti unos
      <br/>
      novih podataka vezanih za volonterske aktivnosti.
      <br />
      U slučaju primjećivanja krivih podataka, obratite se
      <br/>
      osobi s administrativnom ulogom
      <br/> 
     
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
        email:"",
        password:""
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
      this.volonter.email=localStorage.getItem("email");
      this.volonter.password=localStorage.getItem("password");
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

.align{
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

.ogranicenje {
  text-align: center;
  font-size: medium;
  opacity: 65%;
  color: #a020f0;

}
</style>
