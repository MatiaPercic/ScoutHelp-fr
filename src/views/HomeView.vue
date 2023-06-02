<template>
  <div class="home">
    
    <h1 class="title">Dobrodošli na ScoutHelp</h1>
    <p class="plain">Odaberite prijavu ili registraciju za nastavak korištenja stranice</p>

    
    <button type="button" class="btn btn-secondary btn-lg"
      style="
        margin: 2em;
        font-weight: bold;
        font-size: large;
        font-family: Arial;
        color: #A020F0;
        background-color: #fff;
        border-color: #A020F0;
        
      ">
        <router-link style="text-decoration: none;" to="login">Login</router-link>
    </button>

    <button type="button" class="btn btn-secondary btn-lg"
      style="
        margin: 1em;
        font-weight: bold;
        font-size: large;
        font-family: Arial;
        color: #A020F0;
        background-color: #fff;
        border-color: #A020F0;
        
      ">
        <router-link style="text-decoration: none;" to="Register">register</router-link>
    </button>
    </div>
  
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>

< style scoped>

  .home{
    color: #A020F0;
    
  }

</style>