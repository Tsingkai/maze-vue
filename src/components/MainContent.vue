<template>
  <div class="main-content">
    <MapContainer :maze="maze" />
    <MazeInfo
      :size="size"
      :start="startStr"
      :end="endStr"
      @start="searchRoute"
      @restart="restart"
    />
  </div>
</template>

<script>
import MapContainer from '@/components/MapContainer.vue'
import MazeInfo from '@/components/MazeInfo.vue'

export default {
  name: 'MainContent',
  components: {
    MapContainer,
    MazeInfo
  },
  data() {
    return {
      maze: [
        [0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0],
        [0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0],
        [0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 1, 0],
        [0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0],
        [0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0],
        [0, 1, 1, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0],
        [0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0],
        [0, 1, 1, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0],
        [0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0],
        [0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 1, 0],
        [0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0],
        [0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0],
        [0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 1, 0],
        [0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0],
        [0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0],
        [0, 1, 1, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0],
        [0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0],
        [0, 1, 1, 1, 0, 0, 1, 1, 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0],
        [0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0],
        [0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 1, 0]
      ],
      start: [0, 0],
      end: [19, 19],
      route: []
    }
  },
  computed: {
    size() {
      return this.maze.length === 0 ? '0 x 0' : this.maze.length + ' x ' + this.maze[0].length
    },
    startStr() {
      return '( 0 , 0 )'
    },
    endStr() {
      return '(19, 19)'
    }
  },
  methods: {
    restart() {
      location.reload()
    },
    searchRoute() {
      // this.route.push({ x: 0, y: 0 }) // 初始点
      this.findRoad(0, 0)
      const intervalSeed = setInterval(() => {
        if (this.route.length > 0) {
          const route = this.route.pop()
          this.maze[route.x].splice(route.y, 1, 2)
        } else {
          clearInterval(intervalSeed)
        }
      }, 80)

      // this.solveMaze(0, 0) // GPT的方法
    },
    isValidMove(x, y) {
      return x >= 0 && x < this.maze.length && y >= 0 && y < this.maze[0].length && this.maze[x][y] === 0
    },
    solveMaze(x, y) { // 该方法来自chatGPT，看代码应该是深度优先
      console.log(x, y)
      // 辅助函数，用于检查当前位置是否合法

      // 判断是否到达终点
      if (x === this.maze.length - 1 && y === this.maze[0].length - 1) {
        return true
      }

      // 标记当前位置为已访问
      this.maze[x][y] = 2

      // 尝试向四个方向移动
      const directions = [
        [0, 1], // 向右
        [1, 0], // 向下
        [0, -1], // 向左
        [-1, 0] // 向上
      ]

      for (const [dx, dy] of directions) {
        const nextX = x + dx
        const nextY = y + dy
        if (this.isValidMove(nextX, nextY) && this.solveMaze(nextX, nextY)) {
          return true
        }
      }

      // 回溯，标记当前位置为未访问
      this.maze[x][y] = 0

      return false
    },
    findRoad(x, y) { // 自己写的，在ChatGPT帮助下
      if (x < 0 || x >= this.maze[0].length || y < 0 || y >= this.maze.length || this.maze[x][y] !== 0) {
        return false
      }
      if (x === 19 && y === 19) {
        this.formatRoute(x, y)
        return true
      }

      if (!this.isExist(x, y)) {
        this.maze[x][y] = -1
        if (this.findRoad(x + 1, y) || this.findRoad(x - 1, y) || this.findRoad(x, y - 1) || this.findRoad(x, y + 1)) {
          this.formatRoute(x, y)
          return true
        }
      }
      this.maze[x][y] = 0
      this.removeRoute(x, y)
      return false
    },
    formatRoute(x, y) { // 压入路由
      this.route.push({ x: x, y: y })
    },
    isExist(x, y) { // 该点是否已经成为了路径
      return this.route.findIndex(e => e.x === x && e.y === y) !== -1
    },
    removeRoute(x, y) { // 把不是路径的路移除
      const index = this.route.findIndex(e => e.x === x && e.y === y)
      if (index !== -1) {
        this.route.splice(index, 1)
      }
    }
  }
}
</script>

<style scoped>
  .main-content {
    width: 30vw;
    height: 30vw;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    /* gap: 20px; */
    border-radius: 10px;
    backdrop-filter: blur(5px);
    background-color: rgba(0, 191, 255, 0.075);
    box-shadow: rgba(0, 0, 0, 0.3) 2px 8px 8px;
    border: 2px rgba(255, 255, 255, 0.4) solid;
    border-bottom: 2px rgba(40, 40, 40, 0.35) solid;
    border-right: 2px rgba(40, 40, 40, 0.35) solid;
    display: flex;
    flex-direction: column;
    padding: 10px;
  }
</style>
