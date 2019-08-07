<template>
  <div id="app">
    <Dogs></Dogs>
  </div>
</template>

<script>
import Dogs from './components/Dogs.vue'

export default {
  name: 'app',
  components: {
    Dogs
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
