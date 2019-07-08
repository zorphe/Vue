<template>
  <div class="welcome container">
    <div class="card">
      <div class="card-content center-align">
        <h2 class="teal-text">Welcome</h2>
        <form @submit.prevent="enterChat">
          <label for="username">Enter username:</label>
          <input type="text" name="username" v-model="username" />
          <button class="btn teal">Enter Chat</button> 
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Welcome',
  data () {
    return {
      username: null
    }
  }, 
  methods: {
    enterChat(){

    }
  }
}
</script>

<style>
  .welcome{
    max-width: 400px;
    margin-top: 100px;
  }
  .welcome h2{
    font-size: 3em;
  }
  .welcome button{
    margin: 30px auto;
  }
</style>
