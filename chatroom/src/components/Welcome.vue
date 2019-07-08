<template>
  <div class="welcome container">
    <div class="card">
      <div class="card-content center-align">
        <h2 class="teal-text">Welcome</h2>
        <form @submit.prevent="enterChat">
          <label for="username">Enter username:</label>
          <input type="text" name="username" v-model="username" />
          <p v-if="feedback" class="red-text">{{ feedback }}</p>
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
      username: null,
      feedback: null
    }
  }, 
  methods: {
    enterChat(){
      this.feedback = null;

      if (this.username){
        this.$router.push({ name: 'Chat', params: { username: this.username }})
      } else {
        this.feedback = "Please provide a name."
      }
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
  .welcome input{
    text-align: center;
  }
  .welcome button{
    margin: 30px auto;
  }
</style>
