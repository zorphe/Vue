<template>
    <div class="blogs">
        <h2>{{ blogTitle }}</h2>

        <input v-model="searchTerm" />

        <div v-for="post in filteredPosts" :key="post.id">
            <h3>{{ post.title }}</h3>
            <p>{{ post.body | snippet }}</p>
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
            posts: [],
            searchTerm: ''
        }
    },
    methods: {
    },
    computed: {
        filteredPosts(){
            return this.posts.filter(post => {
                return post.title.match(this.searchTerm)
            })
        }
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