<template>
  <nav class="navbar navbar-expand-md navbar-light">
    <a class="navbar-brand" href="/">
      <img
        src="@/assets/wosm.png"
        height="40"
        class="d-inline-block align-top"
        alt=""
      />
    </a>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      
      <form class="navbar-form ml-auto mr-auto">
        <input
          v-model="store.searchTerm"
          class="form-control"
          type="search"
          placeholder="Pretraga"
          aria-label="Search"
        />
      </form>
      
    </div>
  </nav>
 
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #622599;
    }
  }
}
</style>
