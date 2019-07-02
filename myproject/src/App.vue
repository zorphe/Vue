<template>
  <div id="app">
    <h1>{{title}}</h1>

    <Navbar />
    <Blogs />
  </div>
</template>

<script>
import Navbar from './Navbar'
import Blogs from './Blogs'

export default {
  name: 'app',
  components: {
    Navbar,
    Blogs
  },
  data () {
    return {
      title: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
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

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
