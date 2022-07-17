<template>
  <RankingItem />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import RankingItem from './RankingItem.vue'

export default defineComponent({
  name: 'RankingContainer',
  components: {
    RankingItem
  }
});
</script>

<style scoped>
</style>