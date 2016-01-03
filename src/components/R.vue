<template>
    <h1>Image Subreddit Gallery</h1>
    {{sub}}
    {{getImg(sub)}}</template>

<script>

    import http from 'http'

    export default {
        data() {
            return {
                sub: String(window.location).split('/').pop(),
                img: ''
            }
        },
        methods: {
            getImg(sub) {
                //return 'niozn' + sub
                this.$http.get(`https://www.reddit.com/r/${sub}.json`, data => {
                    this.img = data
                })
                .error(err => console.log(err))


                return JSON.stringify(this.img)
            }
        }
    }
</script>

<style>
</style>