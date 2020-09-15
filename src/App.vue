<template>
  <div id="app">
    <MemoryLeak />
  </div>
</template>

<script>
import MemoryLeak from './components/MemoryLeak.vue'

export default {
  name: 'App',
  components: {
    MemoryLeak
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
