<script>
import BarChart from "../components/Charts/BarChart.vue";
</script>

<template>
  <div class="bar">
    <RouterLink to="/pie"></RouterLink>
    <BarChart v-if="retrievedData" :chartData="dogs" />
    <h1>hi</h1>
  </div>
</template>
