<template>
    <div class="add-message">
        <form @submit.prevent="addMessage">
            <label for="new-message">New Message (Enter to add):</label>
            <input type="text" name="new-message" v-model="newMessage"/>
            <p v-if="feedback" class="red-text">{{ feedback }}</p>
        </form>
    </div>
</template>

<script>
import db from '@/firebase/init'

export default {
  name: 'AddMessage',
  props: [ 'username' ],
  data () {
    return {
        newMessage: null,
        feedback: null
    }
  },
  methods: {
      addMessage(){
          if (this.newMessage){
              db.collection('messages').add({
                  content: this.newMessage,
                  username: this.username,
                  timestamp: Date.now()
              }).catch((err) => {
                  console.log(err)
              })

              this.newMessage = this.feedback = null
          } else {
              this.feedback = "Unable to send an empty message"
          }
      }
  }
}
</script>

<style>
</style>
