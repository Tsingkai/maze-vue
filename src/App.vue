<template>
  <div id="app">
    <MainContainer />
  </div>
</template>

<script>
import MainContainer from './components/MainContainer.vue'

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

    width: 100%;
    height: 100%;
  }
</style>
