<template>
    <h1>Image Subreddit Gallery</h1>
    
    <p v-for="link in links">
        <a :href="'r/' + link">r/{{link}}</a>
    </p>
</template>

<script>
    export default {
        data() {
            return {
                links: ['pics', 'wallpaper', 'reactiongifs', 'wallpapers', 'aww', 'cats', 'foxes', 'images', 'memes']
            }
        },
        methods: {
        }
    }
</script>

<style>
</style>