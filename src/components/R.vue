<template>
    <h1>Image Subreddit Gallery</h1>
    {{sub}}
    <br/>
    <br/>
    <br/>
    {{//getImg(sub)}}
    {{testy()}}
</template>

<script>

    import VerEx from 'verbal-expressions'

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
            },

            testy() {
                let content = JSON.stringify(this.img)

                let testhing = 'ame":"t3_3zfx93","created":1451960437,"url":"http://i.imgur.com/9ZgDaaV.jpg","author_flair_'

                /*let truthy = /(https?:\/\/.*\.(?:png|jpg|gif))/i
                console.log(`regex is: ${truthy} and typeof ${typeof truthy}`)*/

                let truthy = VerEx()
                                .startOfLine()
                                .then("http://i.imgur.com/")
                                .anythingBut(" ")
                                .then("jpg")
                                .endOfLine()

                truthy = /(http:\/\/i\.imgur.*jpg)/g
                console.log(truthy)

                let real = testhing.match(truthy)

                console.log(real)

                return testhing
            }
        }
    }
</script>

<style>
</style>