<template>
  <div id="app">
    <h1>{{title}}</h1>

    <Navbar />
    <AllFriends :friends="friends" @delete="removeFriend"/>
    <OnlineFriends :friends="friends" />
  </div>
</template>

<script>
import Navbar from './Navbar'
import AllFriends from './AllFriends'
import OnlineFriends from './OnlineFriends'

export default {
  name: 'app',
  components: {
    Navbar,
    AllFriends,
    OnlineFriends
  },
  data () {
    return {
      title: 'Welcome to Your Vue.js App',
      friends: [
          { name: 'Mario', online: true },
          { name: 'Luigi', online: true },
          { name: 'Toad', online: false },
          { name: 'Bowser', online: false },
          { name: 'Peach', online: false }
      ]
    }
  },
  methods: {
    removeFriend(payload){
      this.friends = this.friends.filter(friend => {
        return friend.name != payload.name
      })
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
