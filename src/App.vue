<template>
  <div id="app">
    <AirbitPlayer audio="/assets/audio/1546533585-28227-thoughts-of-you-drake-type-beat-by-sikwitit-beat.mp3" />
  </div>
</template>

<script>

import AirbitPlayer from './components/AirbitPlayer.vue'

export default {
  name: 'app',
  components: {
    AirbitPlayer
  }
}
</script>

<style>
body{
  padding:0;
  margin:0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 100px;
}
</style>
