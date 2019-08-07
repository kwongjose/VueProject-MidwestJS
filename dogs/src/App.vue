<template>
  <div id="app">
    <nav>
      <router-link to="/about">About</router-link>
      <router-link to="/dogs">Dogs</router-link>
    </nav>
<router-view />
  </div>
</template>

<script>

export default {
  name: 'app',
  components: {

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
#app > div {
 padding: 20px;
}
body {
 margin: 0;
}
nav {
 border-bottom: solid gray 1px;
 padding: 20px;
}
nav a {
 font-size: 24px;
 margin-right: 20px;
 text-decoration: none;
}
nav a.router-link-exact-active {
 color: green;
}
</style>
