<template>
  <div>
      <h1>Countdown Timer</h1>
      <section>

          <div class="hour">
              <h1>{{ hour }}</h1>
              <p>Hours</p>
          </div>

          <div class="min">
              <h1>{{ min }}</h1>
              <p>Minutes</p>

          </div>

          <div class="sec">
              <h1>{{ sec }}</h1>
              <p>Seconds</p>

          </div>

      </section>
    
    <div class="button">
        <button @click="startTimer">Start Timer</button>
        <button @click="stopTimer">Stop Timer</button>
    </div>

  </div>
</template>

<script>
export default {
    name: "Timer",
    props: {
        hour: {
            type: Number,
            default: 0
        },
        min: {
            type: Number,
            default: 0
        },
        sec: {
            type: Number,
            default: 0
        },  
    },
    methods: {
        startTimer() {
            this.$emit('start-timer', true)
            this.timerStarted = !this.timerStarted
        },
        stopTimer() {
            this.timerStarted = !this.timerStarted
            this.$emit('stop-timer', true)

        }
    },
    created() {
        
    },
    data() {
        return {
            timerStarted: false,
            buttonText: "Start Timer"
        }
    }
}
</script>

<style scoped>
    section div {
        display: inline-block;
        margin: 10px 40px;
    }

    button {
        min-width: 500px;
        border: 1px solid lightblue;
        border-radius: 10px;
        padding: 10px;
        background-color: lightseagreen;
        color: white;
        font-weight: bold;
        margin: 0px 10px;
    }
</style>