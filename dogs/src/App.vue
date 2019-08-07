<template>
  <div id="app">
    <Dogs :dogs="dogList"></Dogs>
  </div>
</template>

<script>
import Dogs from './components/Dogs.vue'

export default {
  name: 'app',
  components: {
    Dogs
  },

  data () {
    return {
      dogList: [ { name: "pig" }, { name: "cat" } ]
    }
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
