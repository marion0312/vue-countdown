<template>
  <div id="app">
    <Timer :hour="hour" :sec="sec" @start-timer="countDown" @stop-timer="stopTimer" />
  </div>
</template>

<script>
import Timer from '@/components/Timer';

export default {
  name: 'App',
  data() {
    return {
      hour: 1,
      sec: 50,
      timer: false,
    }
  },  
  components: {
    Timer
  },
  methods: {
    countDown() {
      this.timer = !this.timer
      if ( this.timer ) {
        var interval = setInterval( () => {
            this.sec -= 1
        }, 1000)
      }
      else {
        this.timer = !this.timer
        clearInterval(interval)
      }
    },
    stopTimer() {
      this.sec = 50;
      this.timer = false
    }
  },
  created() {
    // this.countDown();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
