<template>
  <nav class="nav-bar">
    <ul>
        <li><router-link to="/">Home</router-link></li>
        <li><router-link :to="{ name: 'About' }">About</router-link></li>
    </ul>
    <h2>User Profiles</h2>
    <ul>
        <li v-for="(id, idx) in userIds" :key="idx">
            <router-link :to="{ name: 'ViewProfile', params: { user_id: id }}">
                <span>Profile {{ id }}</span>
            </router-link>
        </li>
    </ul>
    <h2>Navigation Controls</h2>
    <ul>
        <button @click="goBack">Go Back</button>
        <button @click="goHome">Redirect to Home</button>
        <button @click="goForward">Go Forward</button>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
  data () {
    return {
      userIds: ['1', '2', '3', '4']
    }
  },
  methods: {
    goBack () {
      this.$router.go(-1)
    },
    goHome () {
      this.$router.push({ name: 'Home' })
    },
    goForward () {
      this.$router.go(1)
    }
  }
}
</script>

<style>
    ul {
        list-style-type: none;
        padding: 0;
    }
    li{
      display: inline-block;
      margin: 10px;
    }
    a{
        color: #42b983;
        padding: 2px;
    }
    a.router-link-exact-active{
      color: purple;
    }
</style>
