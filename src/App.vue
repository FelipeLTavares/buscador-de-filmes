<template>
  <div id="app">
    <Filmes></Filmes>
  </div>
</template>

<script>
import Filmes from './pages/Filmes.vue';

export default {
  name: 'App',
  components: {
    Filmes
}
}
</script>

<style>
body{
  margin: 0;
  padding: 0;
}
#app {
  font-family: 'Rajdhani', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
