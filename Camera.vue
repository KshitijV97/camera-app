<template>
    <div class="camera">
        <video autoplay class="feed"></video>
        <button class="snap" v-on:click="$emit('takePicture')">SNAP</button>
    </div>
</template>

<script>
export default {
    name:"camera",
    methods: {
        init(){
            if('mediaDevices' in navigator && 'getUserMedia' in navigator.mediaDevices){
                let constraints = {
                        video: {
                            width: {
                                min: 640,
                                ideal: 1280,
                                max: 1080
                            },
                            height:{
                                min: 360,
                                ideal: 720,
                                max: 1080
                            }
                        }
                    }
                navigator.mediaDevices.getUserMedia(constraints).then(stream =>{
                    const videoPlayer = document.querySelector("video");
                    videoPlayer.srcObject = stream;
                    videoPlayer.play();
                });
            }
            else{
                alert("Cannot get Media Devices");
            }
        }
    },
    beforeMount(){
        this.init();
    }
}

</script>

<style lang="scss" scoped>
.camera{
    width: 100vh;
    height: 100vh;
    padding: 15px;
    box-sizing: border-box;

    .feed{
        display: block;
        width: 100%;
        max-width: 1280px;
        margin: 0 auto;
        background-color: #171717;
        box-shadow: 6px 6px 12px 0px rgba(0,0,0,0.25);
    }

    .snap{
        display: block;
        width: 75px;
        height: 75px;
        border-radius:50%;
        background-color: transparentize($color: #FFCE00, $amount: 0.5);
        border: 1px solid #171717;
        outline: none;
        margin: 15px auto;

        cursor: pointer;

        &:hover{
            background-color: #FFCE00;
        }

        &:active{
            background-color: darken($color: #FFCE00, $amount: 0.1);
        }
    }
}
</style>

