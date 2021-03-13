<template>
  <div id="app">
    <SetTimer @set-timer="setTimer" />
    <Timer :hour="hour" :min="min" :sec="sec" @start-timer="countDown" @stop-timer="stopTimer" />
  </div>
</template>

<script>
import Timer from '@/components/Timer';
import SetTimer from '@/components/SetTimer';

export default {
  name: 'App',
  data() {
    return {
      hour: 0,
      min: 0,
      sec: 0,
      timer: false,
      interval: '',
    }
  },  
  components: {
    Timer,
    SetTimer
  },
  methods: {
    countDown() {
      this.interval = setInterval( () => {
          if ( this.sec >= 1 )
          {
            this.sec -= 1
          }
          else {
            this.sec = 0
            this.stopTimer()
          }
        }, 1000)
    },
    stopTimer() {
      // this.sec = 50;
      clearInterval(this.interval)
    },
    setTimer(timerSettings) {
      const { hour, min, sec } = timerSettings
      
      this.hour = parseInt(hour)
      this.min = parseInt(min)
      this.sec = parseInt(sec)
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
