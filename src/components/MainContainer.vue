<template>
  <div class="main-container">
    <MainContent />
  </div>
</template>

<script>
import MainContent from '@/components/MainContent.vue'
export default {
  name: 'MainContainer',
  components: {
    MainContent
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .main-container {
    width: 100vw;
    height: 100vh;
    margin: 0;
    padding: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: cadetblue;
  }
</style>
