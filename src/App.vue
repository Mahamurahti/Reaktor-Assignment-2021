<template>
  <div id="app">
    <Home />
  </div>
</template>

<script>
import Home from "@/components/Home";

export default {
  name: 'App',
  components: {
    // This site is an SPA that only displays one element which contains all the other elements
    Home
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Raleway&display=swap');
*{
  margin: 0;
  padding: 0;
}

#app {
  font-family: 'Raleway', sans-serif, Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;

  background-color: #181818;
}
</style>
