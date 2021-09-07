<template>
  <div id="app">
    <Repos msg="Welcome to Your repositories"/>
  </div>
</template>

<script>
import Repos from './components/Repos.vue'

export default {
  name: 'App',
  components: {
    Repos
  },
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
