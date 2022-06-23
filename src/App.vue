<script setup lang="ts">
import { ref } from 'vue';
import LineChart from './components/LineChart.vue';
import Settings from './components/Settings.vue';

const series = ref([]);

function updateChart(data) {
  series.value = data;
}
</script>

<template>
  <h1>Dins2Go</h1>
  <Settings @update:series="updateChart" />
  <LineChart :series="series" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
