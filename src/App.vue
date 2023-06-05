<template>
  <div id="app">
    <nav id="nav" class="navbar" style="background-color: #A020F0;">

      <a class="navbar_title">
        <img src="@/assets/scouthelp.png" 
          alt="" 
          width="90" 
          height="90"
          >ScoutHelp
        </a>
        
      <router-link style="
      text-decoration: none  ;
      font-size: 20px;
      text-align: left;" 
      
      to="login">Login</router-link>  | 

      <router-link style="
      text-decoration: none;
      text-align: left;
      font-size: 20px;"

       to="/about">About</router-link>  | 

       <router-link style="
      text-decoration: none;
      text-align: left;
      font-size: 20px;"

       to="/register">Register</router-link>
    </nav>
    
    <router-view/>
  </div>
</template>

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
  display: flex;
    align-items: center;
 
  
}

.navbar_element {
  font-family: "Arial";
  color: #FFF;
  font-size: 20px;
}

nav {
  
  padding: 5px;
  a {
    font-weight: bold;
    color: #fff;
    
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>

