<script>
<<<<<<< HEAD
import BarChart from "../components/Charts/BarChart.vue";
=======
import BarChart from '../components/Chart/ChartTemplate.vue'
import TheWelcome from '../components/TheWelcome.vue'

export default {
  name: 'App',
  components: { BarChart }
}
>>>>>>> parent of 8e2042d (sanmdas,m)
</script>

<template>
  <div class="bar">
    <RouterLink to="/pie"></RouterLink>
    <BarChart v-if="retrievedData" :chartData="dogs" />
    <h1>hi</h1>
  </div>
</template>
