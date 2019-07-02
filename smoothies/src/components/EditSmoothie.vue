<template>
    <div class="edit-smoothie container">
        <h2 v-if="smoothie" class="center-align indigo-text">Editing {{ smoothie.title }} smoothie</h2>
        <form @submit.prevent="EditSmoothie">
            <div class="field title">
                <label for="title">Smoothie Title:</label>
                <input type="text" name="title" v-model="smoothie.title" />
            </div>
            <div class="field" v-for="(ingredient, idx) in smoothie.ingredients" :key=idx>
                <label for="ingredient">ingredient:</label>
                <input type="text" name="ingredient" v-model="smoothie.ingredients[idx]"/>
                <i class="material-icons remove" @click="removeIngredient(ingredient)">delete</i>
            </div>
            <div class="field add-ingredient">
                <label for="add-ingredient">Add an ingredient:</label>
                <input @keydown.tab.prevent="addIngredient" v-model="another" type="text" name="add-ingredient" />
            </div>
            <div class="field center-align">
                <p v-if="feedback" class="red-text">{{ feedback }}</p>
                <button class="btn pink">Update Smoothie</button>
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
            smoothie: null,
            another: null,
            feedback: null
        }
    },
    created(){
        let ref = db.collection('Smoothies').where('slug', '==', this.$route.params.smoothie_slug)

        ref.get()
            .then((snapshot) => {
            snapshot.forEach((doc) => {
                console.log(doc.data())

                this.smoothie = doc.data()
                this.smoothie.id = doc.id
            })
        })
    },
    methods: {
        EditSmoothie () {
            if (this.smoothie.title){
                this.feedback = null

                // create slug
                this.slug = slugify(this.smoothie.title,{
                    replacement: '-',
                    remove: /[$*_+~.()'"!\-:@]/g,
                    lower: true
                })

                db.collection('Smoothies').doc(this.smoothie.id).update({
                    title: this.smoothie.title,
                    ingredients: this.smoothie.ingredients,
                    slug: this.smoothie.slug
                }).then(() => {
                    this.$router.push({ name: 'Index' })
                }).catch((err) => {
                    console.log(err)
                })
            } else {
                this.feedback = "Please provide a smoothie title"
            }
        },
        addIngredient () {
            if (this.another){
                this.smoothie.ingredients.push(this.another)
                this.another = this.feedback = null
            } else {
                this.feedback = "Please enter a value to add an ingredient"
            }
        },
        removeIngredient (ingredient) {
            this.smoothie.ingredients = this.smoothie.ingredients.filter(currIng => {
                return currIng !== ingredient
            })
        }
    }
}
</script>

<style>
    .edit-smoothie{
        margin-top: 60px;
        padding: 20px;
        max-width: 500px;
    }
    .edit-smoothie h2{
        font-size: 2em;
        margin: 20px auto;
    }
    .edit-smoothie .field{
        margin: 20px auto;
        position: relative;
    }
    .edit-smoothie .remove{
        position: absolute;
        right: 0px;
        bottom: 16px;
        cursor: pointer;
        color: #aaa;
        font-size: 1.4em;
    }
</style>
