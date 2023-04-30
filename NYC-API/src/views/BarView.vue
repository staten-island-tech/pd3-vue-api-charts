<script>
<<<<<<< HEAD
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
=======
import BarChart from "../components/Charts/BarChart.vue";
>>>>>>> parent of ba43d25 (Merge pull request #13 from staten-island-tech/dominic's-up-to-date-branch)
</script>

<template>
  <div class="bar">
    <RouterLink to="/pie"></RouterLink>
    <BarChart v-if="retrievedData" :chartData="dogs" />
    <h1>hi</h1>
  </div>
</template>
