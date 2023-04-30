

<script>
import BarChart from '../components/Chart/ChartTemplate.vue'
import TheWelcome from '../components/TheWelcome.vue'

export default {
  name: 'App',
  components: { BarChart }
}
</script>
<template>
  <main>
    <div class="Bar">
    <BarChart></BarChart>
    </div>
  </main>
</template>

<style scoped>
.Bar{
  width: 100%;
  background-color:black
}
</style>

