<script setup>
import TheWelcome from '../components/TheWelcome.vue'
import BarChart from '../components/Chart/ChartTemplate.vue'

</script>


  <template>
  <BarChart></BarChart>
</template>

<script>
import BarChart from 'path/to/component/BarChart'
import TheWelcome from '../components/TheWelcome.vue'

export default {
  name: 'App',
  components: { BarChart }
}
</script>
<template>
  <main>
    <TheWelcome></TheWelcome>
  </main>
</template>
