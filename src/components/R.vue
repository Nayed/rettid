<template>
    <h1>Image Subrettid Gallery</h1>
    {{sub}}
    <br/>
    <br/>

    <div v-for="pics in getImg(sub)">
        {{ pics }}
        <img src="{{pics}}" width="110" height="90" >
        <a href="{{pics}}" data-lightbox="roadtrip">{{pics}}</a>
    </div>
    
    <!--<div v-for="pics in testy()">
      {{ pics }}
    </div>-->

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

                let truthy = /(http:\/\/i\.imgur.*?jpg)/g

                console.log(JSON.stringify(this.img).match(truthy))
                return JSON.stringify(this.img).match(truthy)
            },

            testy() {
                let content = JSON.stringify(this.img)

                let testhing = 'ame":"t3_3zfx93","created":1451960437,"url":"http://i.imgur.com/9ZgDaaV.jpg","author_flair_http://i.imgur.com/7WElTw6.jpg","author_flair_text":null,"quarantine":false,"title":"Boats on the shore, Thailand [3840*2160]","created_utc":1452175950,"distinguished":null,"mod_reports":[],"visited":false,"num_reports":null,"ups":411}},{"kind":"t3","data":{"domain":"i.imgur.com","banned_by":null,"media_embed":{},"subreddit":"wallpaper","selftext_html":null,"selftext":"","likes":null,"suggested_sort":null,"user_reports":[],"secure_media":null,"link_flair_text":null,"id":"3zyomm","from_kind":null,"gilded":0,"archived":false,"clicked":false,"report_reasons":null,"author":"DietingWays","media":null,"score":13,"approved_by":null,"over_18":false,"hidden":false,"preview":{"images":[{"source":{"url":"https://i.redditmedia.com/x8PFBEGFaFn4rvFlZHP8UbuYXJqA79PR9Jl_ua1jQ5o.jpg?s=a13553b3fe20005e2efabe695f770287","width":1920,"height":1080},"resolutions":[{"url":"https://i.redditmedia.com/x8PFBEGFaFn4rvFlZHP8UbuYXJqA79PR9Jl_ua1jQ5o.jpg?fit=crop&amp;crop=faces%2Centropy&amp;arh=2&amp;w=108&amp;s=cd4b191e244f5435046762692fdde0b9","width":108,"height":60},{"url":"https://i.redditmedia.com/x8PFBEGFaFn4rvFlZHP8UbuYXJqA79PR9Jl_ua1jQ5o.jpgerieio?'

                /*let truthy = /(https?:\/\/.*\.(?:png|jpg|gif))/i
                console.log(`regex is: ${truthy} and typeof ${typeof truthy}`)*/

                let truthy = /(http:\/\/i\.imgur.*?jpg)/g
                //console.log(truthy)

                let real = testhing.match(truthy)

                //console.log(real)

                let m;

                if ((m = truthy.exec(testhing)) !== null) {
                    if (m.index === truthy.lastIndex) {
                        truthy.lastIndex++;
                    }
                } 

                console.log(m)

                return real
            }
        }
    }
</script>

<style>
    div.img {  
    margin: 5px;
    padding: 5px;
    border: 1px solid #0000ff;
    height: auto;
    width: auto;
    float: left;
    text-align: center;
    }

    div.img img {  
        display: inline;
        margin: 5px;
        border: 1px solid #ffffff;
    }

    div.img a:hover img {  
        border:1px solid #0000ff;
    }

    div.desc {  
        text-align: center;
        font-weight: normal;
        width: 120px;
        margin: 5px;
    }

    div.img2 {  
        background-size: contain;
        background-position: 50% 50%;
        background-repeat: no-repeat;
    }
</style>