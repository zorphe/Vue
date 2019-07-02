<template>
    <div class="add-smoothie container">
        <h2 class="center-align indigo-text">Add Smoothie</h2>
        <form @submit.prevent="AddSmoothie">
            <div class="field title">
                <label for="title">Smoothie Title:</label>
                <input type="text" name="title" v-model="title" />
            </div>
            <div v-for="(ingredient, idx) in ingredients" :key=idx>
                <label for="ingredient">ingredient:</label>
                <input type="text" name="ingredient" v-model="ingredients[idx]"/>
            </div>
            <div class="field add-ingredient">
                <label for="add-ingredient">Add an ingredient:</label>
                <input @keydown.tab.prevent="addIngredient" v-model="another" type="text" name="add-ingredient" />
            </div>
            <div class="field center-align">
                <p v-if="feedback" class="red-text">{{ feedback }}</p>
                <button class="btn pink">Add Smoothie</button>
            </div>
        </form>
    </div>
    
</template>

<script>
import db from '@/firebase/init'
import slugify from 'slugify'

export default {
    name: 'AddSmoothie',
    data(){
        return {
            title: null,
            slug: null,
            another: null,
            feedback: null, 
            ingredients: []
        }
    },
    methods: {
        AddSmoothie () {
            if (this.title){
                // create slug
                this.slug = slugify(this.title,{
                    replacement: '-',
                    remove: /[$*_+~.()'"!\-:@]/g,
                    lower: true
                })

                db.collection('Smoothies').add({
                    title: this.title,
                    ingredients: this.ingredients,
                    slug: this.slug
                }).then(()=>{
                    this.$router.push({ name: 'Index' })
                })
            } else {
                this.feedback = "Please provide a smoothie title"
            }
        },
        addIngredient () {
            if (this.another){
                this.ingredients.push(this.another)
                this.another = this.feedback = null
            } else {
                this.feedback = "Please enter a value to add an ingredient"
            }
        }
    }
}
</script>

<style>
    .add-smoothie{
        margin-top: 60px;
        padding: 20px;
        max-width: 500px;
    }
    .add-smoothie h2{
        font-size: 2em;
        margin: 20px auto;
    }
    .add-smoothie .field{
        margin: 20px auto;
    }
</style>
