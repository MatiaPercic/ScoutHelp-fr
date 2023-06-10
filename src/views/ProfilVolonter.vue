<template>
  <div class="about">
    <h3 class="row ">
 
  <div class="row justify-content-between">
    <div class="col-4">
      Osobni podaci:
    </div>
    <div class="col-4">
      Izbornik:
    </div>
  </div>
</h3>
    <p class="plain">Ime: {{ volonter.ime }}</p>
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
      },
    };
  },

  mounted() {
    this.info();
  },

  methods: {
    info() {
      this.volonter.ime = localStorage.getItem("ime");
    },
  },
};
</script>

<style scoped>
.plain {
  text-align: justify;
  padding-left: 10px;
  font-size: 20px;
  margin-left: 20px;
}

.title{
  
  text-align: left;
  margin-left: 3%;
  margin-top: 3%;
  
}

.plain_text{
  text-align: right;
  margin-left: 30px;
  margin-top: 25px;
  margin-left: 4%;
  margin-top: 1%;
}
</style>
