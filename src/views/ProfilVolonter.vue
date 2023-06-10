<template>
  <div class="about">
    <h1>Profilna stranica za volontere</h1>
    
    <p class="plain">
     Ime:  {{ volonter.ime }}
    </p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "profilVolonter",

  data() {
    return {
      volonter: {
        ime: ""
      }
    };
  },

  mounted() {
    this.info();
  },

  methods: {
    info() {
      this.volonter.ime = localStorage.getItem('ime');
    }
  }
};
</script>
