<template>
    <div id="online-friends">
        <h2>Online Friends</h2>
        <div v-for="(friend, idx) in friends" :key="idx">
            <span v-if="friend.online"> {{friend.name}} </span>
        </div>
    </div>
</template>

<script>

export default {
    name: 'OnlineFriends',
    props: ['friends'],
    data() {
        return {
        }   
    }
}
</script>

<style>

</style>