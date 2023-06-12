<template>
  <div id="app">
    <nav
      class="navbar navbar-expand-lg navbar-light"
      style="background-color: #a020f0"
    >
      <a class="navbar_title">
        <img src="@/assets/scouthelp.png" alt="" height="60" />ScoutHelp
      </a>
      <ul class="navbar-nav mr-auto mt-2 mt-lg-0">

      <li v-if="!loggedIn" class="navbar_element">
          <router-link style="text-decoration: none" to="/">Login</router-link>
        </li> 
        

        
        <li v-if="!loggedIn" class="navbar_element">
          <router-link style="text-decoration: none" to="/register"
            >Register</router-link
          >
        </li>
<!--         <li  v-if="loggedIn" v-on:click="profilCheck()" class="navbar_element">
            <a>Profil</a>
        </li>
 -->
        <li v-if="profilvol" v-on:click="check()" class="navbar_element">
          <router-link style="text-decoration: none" to="/profilVolonter"
            >Profil</router-link
          >
        </li>
        <li v-if="profiladm" v-on:click="check()"  class="navbar_element">
          <router-link style="text-decoration: none" to="/profilAdmin"
            >Profil</router-link
          >
        </li>
        <li  v-on:click="check()" class="navbar_element">
          <router-link style="text-decoration: none" to="/about"
            >About</router-link
          >
        </li>

        <li v-if="loggedIn" v-on:click="logout()" class="navbar_element">
          <a style="text-decoration: none">Logout</a>
        </li>
      </ul>
    </nav>

    <router-view />
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      loggedIn: false,
      profilvol:false,
      profiladm:false
    };
  },

  created(){

    this.check()
  },
  watch:{
    loggedIn(){
      this.check()
    },
    profilvol(){
        this.check()
    },
    profiladm(){
      this.check()
    }
  },
  async mounted() {},
  methods: {
    logout() {
      console.log(this.loggedIn);
      localStorage.clear();
      console.log(localStorage.getItem("ime"));
      this.loggedIn = false;
      console.log(this.loggedIn);
      this.profiladm=false;
      this.profilvol=false;
      this.$router.push({ name: "login" });
    },

    
    check(){
      let admin=localStorage.getItem("pozicija");
      let provjera=localStorage.getItem("ime");
      console.log(provjera," ",admin);
      if(provjera){
        if(admin)
          this.profiladm=true;

        else this.profilvol=true;

        this.loggedIn=true;
      }
      else{
        this.profiladm=false;
        this.profilvol=false;
        this.loggedIn=false;
      }
        


      
      /* if(provjera && this.$route.path!=="/profilAdmin")
        this.$router.replace({name:"profilAdmin"});

      else if(!provjera && this.$route.path!=="/profilVolonter")
        this.$router.replace({name:"profilVolonter"});

      else 
        return; */
      

    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.navbar_title {
  text-align: left;
  font-family: "Arial";
  color: #fff;
  font-size: 40px;
  padding-right: 62%;

  align-items: center;
  &:hover{
    color:#fff;
  }
}

.navbar_element {
  text-align: right;
  font-family: "Arial";
  color: #fff;
  font-size: 13px;
  margin-left: 10px;
  text-decoration: none;


}

nav {
  padding: 50px;
  a {
    font-weight: bold;
    color: #fff;
    text-align: right;
    font-size: 27px;
    margin-right: 0;
    transition: color 0.3s;
  &:hover{
    color:aquamarine;
  }
    &.router-link-exact-active {
      color:yellow;
    }
  }
}
</style>
