<template>
  <div id="app">
    <game-grid />
  </div>
</template>

<script>
import GameGrid from './components/GameGrid.vue'

export default {
  name: 'app',
  components: {
    "game-grid": GameGrid
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
