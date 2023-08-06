<template>
  <div class="maze-info">
    <span>地图尺寸：{{ size }}</span>
    <span>开始坐标：{{ start }}</span>
    <span>目的坐标：{{ end }}</span>
    <button class="btn circle" @click="startFind"> 开始 </button>
    <button class="btn circle-reset" @click="restart"> 再来一次 </button>
  </div>
</template>

<script>
export default {
  name: 'MazeInfo',
  props: {
    size: {
      type: String,
      default: '0 x 0',
      required: true
    },
    start: {
      type: String,
      default: '(0 , 0)',
      required: true
    },
    end: {
      type: String,
      default: '(0 , 0)',
      required: true
    }
  },
  methods: {
    startFind() {
      this.$emit('start')
    },
    restart() {
      this.$emit('restart')
    }
  }
}
</script>

<style scoped>
  .maze-info {
    display: flex;
    flex-direction: column;
    flex: auto;
    justify-content: center;
    align-items: center;
    width: 60%;
  }

  .btn {
    width: 180px;
    height: 30px;
    overflow: hidden;
    margin: 10px;
  }

  .circle {
    background-color: #60cc60;
    color: #fff;
    position: relative;
    z-index: 1;
    overflow: hidden;
    border: 0 solid transparent;

    border-radius: 10px;
  }

  .circle::before {
    content: "";
    position: absolute;
    z-index: -1;
    top: 50%;
    left: 50%;
    width: 1rem;
    height: 1rem;
    transform: translate3d(-50%, -50%, 0) scale(0, 0);
    border-radius: 50%;
    background-color: #45aa45;
    transform-origin: center;
    transition: ease-in-out 0.5s;
  }

  .circle:hover::before {
    transform: translate3d(-50%, -50%, 0) scale(15, 15);
  }

  .circle-reset {
    background-color: #cc6060;
    color: #fff;
    position: relative;
    z-index: 1;
    overflow: hidden;
    border: 0 solid transparent;

    border-radius: 10px;
  }

  .circle-reset::before {
    content: "";
    position: absolute;
    z-index: -1;
    top: 50%;
    left: 50%;
    width: 1rem;
    height: 1rem;
    transform: translate3d(-50%, -50%, 0) scale(0, 0);
    border-radius: 50%;
    background-color: #aa4545;
    transform-origin: center;
    transition: ease-in-out 0.5s;
  }

  .circle-reset:hover::before {
    transform: translate3d(-50%, -50%, 0) scale(15, 15);
  }
</style>
