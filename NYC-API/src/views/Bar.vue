<script>
import {Barchart} from '../components/Chart/ChartTemplate.vue'

  
  import { Bar } from 'vue-chartjs'
  import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'


  
  ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)
  
  
</script>
<template>
     <Bar :data="chartData" :options="chartOptions" v-if="retrievedData" />
  </template>
  