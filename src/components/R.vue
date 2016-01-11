<template>
    <h1>Image Subrettid Gallery</h1>
    {{sub}}
    <br/>
    <br/>

    <div v-for="pics in getImg(sub)">
        <div class="img">
            <!--{{ pics }} -->
            <a href="{{pics}}" data-lightbox="{{pics}}">
                <img src="{{pics}}" width="110" height="90" >
            </a>
        </div>
    </div>
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

                let truthy = /(http:\/\/i\.imgur\.com\/[a-zA-Z0-9]+\.jpg)/g

                console.log(JSON.stringify(this.img).match(truthy))
                return JSON.stringify(this.img).match(truthy)
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