

<script>
import BarChart from '../components/Charts/ChartTemplate.vue'


export default {
  name: 'App',
  components: { BarChart }
}
</script>
<template>
  <main>
    <div class="Bar">
    <BarChart>Birthyear</BarChart>
    </div>
  </main>
</template>

<style scoped>
.Bar{
  width: 100%;
  background-color:darkgray;
  
  
}
</style>

