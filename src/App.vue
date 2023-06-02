<template>
  <div id="app">
    <nav class="navbar navbar-light" style="background-color: #A020F0;">
      <p class="navbar_title">ScoutHelp</p>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
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
  text-align: center;
  font-family: "Arial";
  color: #fff;
  font-size: 30px;
}

.navbar_element {
  font-family: "Arial";
  color: #FFF;
  font-size: 40px;
  margin: 10px;
}

nav {
  padding: 20px;

  a {
    font-weight: bold;
    color: #fff;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
