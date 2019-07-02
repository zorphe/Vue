<template>
    <div class="blogs">
        <h2>{{ blogTitle }}</h2>

        <div v-for="post in posts" :key="post.id">
            <h3>{{ post.title }}</h3>
            <p>{{ post.body }}</p>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Blogs',
    data(){
        return {
            blogTitle: 'Blogs',
            posts: []
        }
    },
    methods: {
    },
    created(){
        // can swap to async + await syntax instead?
        axios.get('https://jsonplaceholder.typicode.com/posts')
            .then(response => {
                this.posts = response.data
            })
            .catch(err => {
                console.log(err)
            })
    }
}
</script>

<style>

</style>