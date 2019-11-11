<template>
  <div class="airbit-player">
    <div class="player-buttons">
        <button :class="{'pause': isPlaying,'play-btn':true }" @click="play"></button>
    </div>
    <div class="player-container">
        <div id="waveform"></div>
        <div class="timer">
            <div class="currentpost">{{ convertHMS(currentPos) }}</div>
            <div class="length">{{ convertHMS(length) }}</div>
        </div>
    </div>
  </div>
</template>

<script>
import WaveSurfer from 'wavesurfer.js'

export default {
  name: 'AirbitPlayer',
  data:function(){
      return {
           isPlaying: false,
           currentPos : 0,
           length:0
      }
  }  ,
  props: {
    audio: String
  },
  mounted () {
    
        this.$nextTick(() => {
        this.wavesurfer = WaveSurfer.create({
            container: '#waveform',
            waveColor: 'white',
            progressColor: 'white',
            barWidth: 2,
            cursorWidth:2,
            cursorColor: '#9e36bf',
            progressColor: '#9e36bf',
            responsive: true,
            barRadius:2,
            
        })
            let wavesurfer = this.wavesurfer
            let _this = this
            wavesurfer.load(this.audio);
            wavesurfer.on('audioprocess', function(){
                _this.currentPos =  wavesurfer.getCurrentTime();
            })
            wavesurfer.on('ready', function(){
                _this.length =  wavesurfer.getDuration();
            })
            
        })
  },
   methods: {
    convertHMS(value) {
        const sec = parseInt(value, 10); // convert value to number if it's string
        let hours   = Math.floor(sec / 3600); // get hours
        let minutes = Math.floor((sec - (hours * 3600)) / 60); // get minutes
        let seconds = sec - (hours * 3600) - (minutes * 60); //  get seconds
        // add 0 if value < 10
        if (hours   < 10) {hours   = "0"+hours;}
        if (minutes < 10) {minutes = "0"+minutes;}
        if (seconds < 10) {seconds = "0"+seconds;}
        return hours+':'+minutes+':'+seconds; // Return is HH : MM : SS
    },
  	play () {
    	this.wavesurfer.playPause()
        console.log(this.isPlaying)
        this.isPlaying = !this.isPlaying
    }
  }
  
}
</script>



<style scoped>
.airbit-player{
    padding: 50px 0;
    background: url(../assets/audio-bg.jpg) center center;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
    -ms-flex-direction: row;
    flex-direction: row;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    background-size: cover;
    
}
.player-buttons{
    padding:0 30px;
}
.player-container{
    flex-grow:1;
}
.play-btn{
    border: 1px solid #fff;
    background: transparent;
    height: 40px;
    width: 40px;
    border-radius: 50%;
    background-size: 16px 16px;
    background-position: 58% 50%;
    background-repeat: no-repeat;
    text-align: center;
    background-image:url(../assets/play-button.png);
    cursor:pointer;
}
.play-btn:hover{

    background-color:rgba(255,255,255,.2)
}
.play-btn:active{
    outline:none;
}
.play-btn.pause{
    background-image:url(../assets/pause-button.png);
    background-position: 50% 50%;
}
 
.currentpost,.length{
    color:#fff;
    font-size:14px;
}
.currentpost{float:left}
.length{float:right}
</style>
