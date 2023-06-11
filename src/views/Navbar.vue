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
          <li  class="navbar_element">
            <router-link style="text-decoration: none;"  to="/"
              >Login</router-link
            >
          </li>
  
          <li  class="navbar_element">
            <router-link
              style="text-decoration: none; "
              to="/register"
              >Register</router-link
            >
            
          </li>
          <li class="navbar_element">
            <router-link
              style="
                text-decoration: none;
  
               
              "
              to="/about"
              >About</router-link
            >
          </li>
  
          <li class="navbar_element">
            <a style="text-decoration: none;"  to="/"
              >
            LogOut
            </a>
          </li>
        </ul>
      </nav>
  
      <router-view />
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
  