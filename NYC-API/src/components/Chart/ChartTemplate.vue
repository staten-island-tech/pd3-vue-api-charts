<template>
    <Bar
      v-if="loaded"
      id="my-chart-id"
      :options="chartOptions"
      :data="chartData"
    />
  </template>
  
  <script>
  import { Bar } from 'vue-chartjs'
  import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'

  
  ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)
  

  export default {
    name: 'BarChart',
    components: { Bar },
    data() {
      return {
       
        chartData: {
          labels: [],
          datasets: []
        },
        chartOptions: {
          responsive: true
        },
            loaded: false,
      }
      
    },
    
  
mounted() {
    this.getCD();
 
  },
  methods: {
 
   getCD: async function  () {
      
 let dates = [];
  
      let label = [];
      
      this.loaded = false;
      try {
        let api = await fetch(
          "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
        );
        let object=await api.json()
       console.log(dates)
        object.forEach((dog=>{
          let birth=dog.animalbirth
          dates.push(birth)
         
        }))
    let x= new Set(dates)
    x.forEach((birth)=>{
      label.push(birth)
    })
    this.loaded = true;
    console.log(x)
this.chartData.datasets.push(dates)
         this.chartData.labels.push(label)
      }
        
      
      catch (error) {
        console.log(error);
      }
       
  },
  

  }
  }
  
  
  
  </script>