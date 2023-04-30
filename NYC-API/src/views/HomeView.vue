

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
    <BarChart>Birthyear</BarChart>
    </div>
  </main>
</template>

<style scoped>
.Bar{
  width: 100%;
  background-color:white;
  font-family: 'Times New Roman', Times, serif;
  -webkit-text-fill-color:gold
  
}
</style>

