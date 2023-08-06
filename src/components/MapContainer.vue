<template>
  <div class="map-container">
    <div class="map">
      <div v-for="(row, index) in maze" :key="index" class="row">
        <MapItem v-for="(column, indexCol) in row" :key="index+ ' ' + indexCol" :cellValue="column"  />
      </div>
    </div>
  </div>
</template>

<script>
import MapItem from '@/components/MapItem.vue'
export default {
  name: 'MapContainer',
  components: {
    MapItem
  },
  props: {
    maze: {
      type: Array,
      default: null,
      required: true
    }
  }
}
</script>

<style scoped>
  .map-container {
    width: 60%;
    min-width: 220px;
    height: 60%;
    min-height: 220px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .map{
    display: flex;
    flex-direction: column;
  }

  .row{
    display: flex;
    flex-direction: row;
  }
</style>
