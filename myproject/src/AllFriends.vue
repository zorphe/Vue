<template>
    <div id="all-friends">
        <h2>All Friends</h2>
        <div v-for="(friend, idx) in friends" :key="idx">
            <span @click="unfriend(friend.name)">{{ friend.name }}</span>
        </div>
    </div>
</template>

<script>

export default {
    name: 'AllFriends',
    props: ['friends'],
    data() {
        return {
        }
    },
    methods: {
        unfriend(name){
            this.$emit('delete', { name })
        }
    }
}
</script>

<style>

</style>