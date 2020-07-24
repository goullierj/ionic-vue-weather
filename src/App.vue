<template>
  <div id="app">
    <div id="nav">
      <h1>WEATHER API</h1>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: black;
}

#nav {
  padding: 5px;

  h1 {
    margin: 0;
    font-weight: bold;
    color: white;
    font-size: 15px;
    padding: 10px;
  }
}
</style>
