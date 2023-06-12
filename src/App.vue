<template>
  <div id="app">
    <nav
      class="navbar navbar-expand-lg navbar-light"
      style="background-color: #a020f0"
    >
      <a class="navbar_title">
        <img src="@/assets/scouthelp.png" alt="" height="50" />ScoutHelp
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
        <li v-if="profilvol" v-on:click="profilCheck()"  class="navbar_element">
          <router-link style="text-decoration: none" to="/profilVolonter"
            >Profil</router-link
          >
        </li>
        <li v-if="profiladm" v-on:click="profilCheck()"  class="navbar_element">
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
    this.profilCheck()
  },
  watch:{
    loggedIn(){
      this.check()
    },
    profilvol(){
        this.profilCheck()
    },
    profiladm(){
      this.profilCheck()
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
    check() {
      if (localStorage.length > 0) {
        console.log(localStorage.getItem("prezime"));
        this.loggedIn = true;
        console.log(this.loggedIn);
      } else {
        this.loggedIn = false;
        console.log(this.loggedIn);
      }
    },
    
    profilCheck(){
      let admin=localStorage.getItem("pozicija");
      let provjera=localStorage.getItem("ime");
      console.log(provjera," ",admin);
      if(provjera){
        if(admin)
          this.profiladm=true;

        else this.profilvol=true;
      }
      else{
        this.profiladm=false;
        this.profilvol=false;
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
  font-size: 30px;
  padding-right: 50%;

  align-items: center;
}

.navbar_element {
  text-align: right;
  font-family: "Arial";
  color: #fff;
  font-size: 15px;
  margin-left: 5px;
  text-decoration: none;
}

nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #fff;
    text-align: right;
    font-size: 20px;
    margin-right: 0;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
