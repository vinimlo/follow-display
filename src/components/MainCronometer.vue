<template>
  <div id="cronometer-container">
    <strong id="cronometer">{{ (minutes > 9 ? minutes : "0" + minutes) + ":" + (seconds > 9 ? seconds : "0" + seconds) + "."
        + (milliseconds > 9 ? (milliseconds > 99 ? milliseconds : "0" + milliseconds) : "00" + milliseconds)
    }}</strong>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'MainCronometer',
  props: {
    isTimeRunning: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      startTime: 0,
      elapsedTime: new Date().getTime(),
      finishedTime: 0,
      cronometerExecution: 0,
      minutes: 0,
      seconds: 0,
      milliseconds: 0,
      started: 0
    }
  },
  methods: {
    start() {
      this.reset()
      this.startTime = new Date().getTime();
      this.started = setInterval(this.clockRunning, 10);
    },
    stop() {
      this.finishedTime = new Date().getTime();

      clearInterval(this.started);
    },
    reset() {
      clearInterval(this.started);
      this.startTime = 0;
      this.finishedTime = 0;
      this.elapsedTime = 0;
    },
    toggleTime() {
      if (!this.isTimeRunning) {
        this.start();
      } else if (this.isTimeRunning) {
        this.stop();
      }
    },
    clockRunning() {
      let currentTime = new Date().getTime();
      this.elapsedTime = new Date(currentTime - this.startTime - this.finishedTime).getTime();
      this.minutes = Math.floor((this.elapsedTime) / 60000);
      this.seconds = Math.floor((this.elapsedTime) / 1000) % 60;
      this.milliseconds = (this.elapsedTime % 1000);
    }
  }
});
</script>

<style scoped>
#cronometer-container {
  width: 100%;
  text-align: center;
}

#cronometer {
  font-size: 12vw;
  font-weight: 500;
  color: #FFFFFF;
}

@media only screen and (max-width: 968px) {
  #cronometer {
    font-size: 20vw;
  }
}
</style>