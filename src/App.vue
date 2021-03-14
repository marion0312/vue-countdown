<template>
  <div id="app">
    <SetTimer @set-timer="setTimer" />
    <Timer 
    :startDisabled="startDisabled"
    :stopDisabled="stopDisabled"
    :timerName="timerName" 
    :hour="hour" 
    :min="min" 
    :sec="sec" 
    @start-timer="countDown" 
    @stop-timer="stopTimer" />

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
      timerName: 'Countdown Timer',
      startDisabled: true,
      stopDisabled: true,
    }
  },  
  components: {
    Timer,
    SetTimer
  },
  methods: {
    countDown() {
      this.startDisabled = !this.startDisabled
      this.stopDisabled = !this.stopDisabled
      this.interval = setInterval( () => {
        if ( this.sec >= 1 )
          {
            this.sec -= 1
          }
          else {
            this.sec = 0
            // IF MINS EXIST, MINS -1
            if ( this.min > 0 )
            {
              // RESET SECONDS TO 60
              this.sec = 60
              this.min -= 1

            }
            // IF HOUR IS NOT 0, HOUR -1
            else if ( this.hour > 0 )
            {
              this.min = 60
              this.hour -= 1
            }
            else
            {
              this.startDisabled = !this.startDisabled
              this.stopDisabled = !this.stopDisabled
              this.stopTimer()
            }
          }
        }, 1000)
    },
    stopTimer() {
      // this.sec = 50;
      this.startDisabled = false
      this.stopDisabled = true
      clearInterval(this.interval)
    },
    setTimer(timerSettings) {
      const { hour, min, sec, timerName } = timerSettings

      
      this.hour = parseInt(hour)
      this.min = parseInt(min)
      this.sec = parseInt(sec)
      this.timerName = timerName
      if ( this.hour != 0 || this.min != 0 || this.sec != 0 )
      {
        this.startDisabled = !this.startDisabled
      }
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
