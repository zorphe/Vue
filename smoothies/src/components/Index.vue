<template>
  <div class="index container">
    <div class="card" v-for="smoothie in smoothies" :key="smoothie.id">
      <div class="card-content">
        <i class="material-icons remove" @click="removeSmoothie(smoothie.id)">delete</i>
        <h2 class="indigo-text">{{ smoothie.title }}</h2>
        <ul class="ingredients">
          <li v-for="(ingredient, idx) in smoothie.ingredients" :key="idx">
            <span class="chip">{{ ingredient }}</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import db from '@/firebase/init'

export default {
  name: 'Index',
  data () {
    return {
      smoothies: []
    }
  },
  methods: {
    removeSmoothie(id){
      //delete doc from db
      db.collection('Smoothies').doc(id).delete()
        .then(() => {
          this.smoothies = this.smoothies.filter((smoothie) => {
          return smoothie.id != id
          })
        })
    }
  },
  created () {
    //fetch data
    db.collection('Smoothies').get()
      .then((snapshot) => {
        snapshot.forEach((doc) => {
          console.log(doc.data())

          let smoothie = doc.data()
          smoothie.id = doc.id
          this.smoothies.push(smoothie)
        })
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .index{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 30px;
    margin-top: 60px;
  }
  .index h2{
    font-size: 1.8em;
    text-align: center;
    margin-top: 0;
  }
  .index .ingredients{
    margin: 30px auto;
  }
  .index .ingredients li{
    display: inline-block;
  }

  .index .remove{
    position: absolute;
    top:4px;
    right: 4px;
    cursor: pointer;
    color: #aaa;
    font-size: 1.4em;
  }
</style>
