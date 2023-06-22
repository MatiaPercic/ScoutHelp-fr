<template>
  <div class="about">
    <h1>Odabir dobnih skupina s kojima radiš/želiš raditi</h1>

    <h3>Trenutne dobne skupine:</h3>


    <span
      v-for="dobne in stare_dobne_skupine"
      v-if="dobne"
      class="custom_span">
   {{ dobne }}
    </span>
    
    <div class="container custom">
      <div v-for="item in dobneLista" :key="item.id">
        <label :for="item.id" class="form-check-label">{{
          item.dobna_skupina
        }}</label>
        <input
          type="checkbox"
          :id="item.id"
          v-model="item.checked"
          class="form-check-input"
        />
      </div>
    </div>

    <div class="d-grid gap-2 d-md-block">
      <button type="button" @click="buttonProfil()" class="btn btn-primary">
          Povratak na profil
        </button>

      <button class="btn btn-primary" @click="unesiPromijene()">Unesi promijene</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "dobneSkupine",

  data() {
    return {
      volonter: {
        email: "",
        dobne_skupine_rada: [],
       
      },
      dobneLista: [],
      stare_dobne_skupine: [],
    };
  },
  mounted() {
    this.volInfo();
    this.getDobneLista();
  },
  methods: {
    volInfo() {
      this.volonter.email = localStorage.getItem("email");
      this.stare_dobne_skupine =
        localStorage.getItem("dobne_skupine_rada");
    },

    getDobneLista() {
      axios.get("https://scouthelp-f893.onrender.com/dobneSkupine").then((response) => {
        this.dobneLista = response.data.map((item) => ({
          dobna_skupina: item.dobna_skupina,
          _id: item._id,
          checked: false,
        }));
        console.log(this.dobneLista);
      });
    },
    buttonProfil(){
      this.$router.push({
        name:"profilVolonter"
      });
    },
    unesiPromijene(){
        this.volonter.dobne_skupine_rada=this.dobneLista.filter(item=>item.checked).map(item=>item.dobna_skupina);

        axios
        .put("https://scouthelp-f893.onrender.com/updateDobneSkupine", this.volonter)
        .then((response)=>{
            console.log(response.data);
            alert ("Uspiješno promijenjene dobne skupine s kojima želite raditi - pritisni ok za povratak na profil ")

        this.$router.push({
            name:"profilVolonter"
        });
        });
    }
  },
};
</script>

<style scoped>
h1 {
  margin-top: 30px;
}

h3 {
  margin-top: 40px;
}
.custom_span {
  white-space: nowrap;
}

.custom {
  margin-top: 50px;
  margin-bottom: 50px;
}

.form-check-label {
  font-size: 30px;
}

.form-check-input {
  --bs-form-check-bg: var(--bs-form-check-bg);
  vertical-align: inherit;
  width: 1.5em;
  height: 1.5em;
  margin-left: 1em;
  border-color: #a020f0;
  border-width: 2px;
}

.form-check-input:checked {
  border-color: #fff;
  background-color: #a020f0;
}

button {
  margin-top: 30px;
  font-weight: bold;
  font-size: larger;
  font-family: Arial;
  color: #a020f0;
  background-color: #fff;
  border-color: #a020f0;
  margin-left: 10px;
}

.btn:hover {
  background-color: #a020f0;
  color: #fff;
}

</style>
