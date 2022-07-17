<template>
  <main @click="toggleTime">
    <section class="row" id="top-row">
      <MainCronometer ref="mainCronometer" :isTimeRunning="isTimeRunning" />
    </section>
    <section class="row" id="bottom-row">
      <RankingContainer />
    </section>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import MainCronometer from './components/MainCronometer.vue'
import RankingContainer from './components/RankingContainer.vue'

export default defineComponent({
  name: 'App',
  components: {
    MainCronometer,
    RankingContainer
  },
  data() {
    return {
      isTimeRunning: false
    }
  },
  methods: {
    toggleTime() {
      this.isTimeRunning = !this.isTimeRunning;
      (this.$refs['mainCronometer'] as typeof MainCronometer).toggleTime();
    }
  }
});
</script>

<style>
body {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
  font-family: sans-serif;
}

main {
  width: 100%;
  height: auto;
}

.row {
  width: 100%;
}

#top-row {
  background-color: #0097a7;
  height: 50vh;
}

#bottom-row {
  background-color: #f2f2f2;
  height: 50vh;
}
</style>
