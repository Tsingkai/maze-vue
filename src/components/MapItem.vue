<template>
  <div class="map-item" :style="backgroundColor"></div>
</template>

<script>
export default {
  name: 'MapItem',
  props: {
    cellValue: {
      type: Number,
      default: 0,
      required: true
    }
  },
  computed: {
    backgroundColor() {
      let color = 'background-color:'
      switch (this.cellValue) {
        case 0: // road
          color += 'lightgray'
          break
        case 1: // wall
          color += 'darkslategrey'
          break
        case 2: // result
          color += 'orange'
          break
        default:
          color += 'lightgray'
          break
      }
      return color
    }
  }
}
</script>

<style scoped>
  .map-item {
    width: 10px;
    height: 10px;
  }
</style>
