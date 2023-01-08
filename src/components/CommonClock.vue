<template>
  <div class="container">
      <div class="clock-inner" :class="color">
        <div class="hour">{{hours}}</div>
        <div class="dots">:</div>
        <div class="min">{{minutes}}</div>
        <div class="dots">:</div>
        <div class="secs">{{seconds}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DigitalClock',
  props: {
    color: {
      type: String,
      default: 'red'
    }
  },
  data () {
    return {
      hours: 0,
      minutes: 0,
      seconds: 0
    }
  },
  methods: {
    setTime () {
      setInterval(() => {
        const date = new Date()
        this.hours = date.getHours()
        this.minutes = this.checkSingleDigit(date.getMinutes())
        this.seconds = this.checkSingleDigit(date.getSeconds())
      }, 1000)
    },
    checkSingleDigit (digit) {
      return ('0' + digit).slice(-2)
    }
  },
  mounted () {
    this.setTime()
  }
}
</script>

<style>
.container {
    display: flex;
    color: hsl(8, 60%, 92%);
    margin-bottom: 7px;
}

.clock-inner {
    display: flex;
    margin: 0 auto;
}
</style>