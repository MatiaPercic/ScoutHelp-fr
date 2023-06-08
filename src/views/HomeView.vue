<template>
  <div class="home">
    
    <h1 class="title">Dobrodošli na ScoutHelp</h1>
    
 <div id="app">

  <div v-for="v in volonteri" :key="v">
    {{ v.ime }}
    {{ v.prezime }}
    {{ v.email }}
    {{ v.godine }}
    {{ v.br_aktivnosti }}
    {{ v.br_sati }}

 </div>
</div>

  </div>
  
</template>

<script>
// @ is an alias to /src


console.log("outside mounted : ");

export default {
  name: 'HomeView',
 
  
  async mounted() {
    
    let response = await fetch("http://localhost:3001/volonteri");
    console.log("in mounted: ");
    console.log(response);
  },
  
  data() {
    return {
      volonteri: [],
    };
  }
}


</script>

< style scoped>

  .home{
    color: #A020F0;
    
  }

</style>