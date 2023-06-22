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
        margin: 1em;
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

    <button
      type="button"
      class="btn btn-primary"
      style="
        margin: 1em;
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
        to="/dobneSkupine"
        >Postava dobnih skupina</router-link
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

<div>
  <b-alert show variant="warning" v-if="showWarn" class="alert">
    <router-link to="/dobneSkupine" class="alert-link">
      Lista rada sa željenim dobnim skupinama je prazna - promijeniti radi evidencije!
    </router-link>
  </b-alert>
</div>

</div>
</template>

<script>
import axios from "axios";


export default {
   name: "profilVolonter",
  data() {
    return {
      volonter: {
        ime: "",
        prezime: "",
        godine: null,
        broj_aktivnosti: null,
        broj_volonterskih_sati: null,
        email:"",
        password:"",
        dobne_skupine_rada:[]
      },
      showWarn:false,
    };
  },

  mounted() {
    this.info();
    this.dobneGet();

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
      console.log(this.volonter.broj_aktivnosti);
    },





    dobneGet(){
        axios
        .post("https://scouthelp-f893.onrender.com/dobneVolontera",this.volonter)
        .then((response)=>{
          this.volonter.dobne_skupine_rada=response.data.dobne_skupine_rada;
          console.log(this.volonter.dobne_skupine_rada);
          localStorage.setItem("dobne_skupine_rada",this.volonter.dobne_skupine_rada);
          if(this.volonter.dobne_skupine_rada.length==0)
                this.showWarn=true;
        });
      }
  },
};
</script>

<style scoped>

.about {
  overflow-x: hidden;
}


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
  margin-top: 30px;
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

.alert{
  margin-top: 20px;
}
</style>
