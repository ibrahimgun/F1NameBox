<template>
  <div id="app">
    <div id="nav">
     
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
    @import url("https://fonts.googleapis.com/css2?family=Inter:wght@500&display=swap");
  font-family: "Inter", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
