<template>
  <div id="app">
    <MainContainer msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import MainContainer from './components/Main.vue'

export default {
  name: 'App',
  components: {
    MainContainer
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
