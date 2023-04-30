<template>
     <Bar :data="chartData" :options="chartOptions" v-if="retrievedData" />
  </template>
  
  <script>
  import { Bar } from 'vue-chartjs'
  import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'

  
  ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)
  

  export default {
    name: "Barchart",
    components: { Bar },
    data() {
      return {
        chartData: {
          labels: [ birth ],
          datasets: [ { data: [] } ]
        },
        chartOptions: {
          responsive: true
        },
            retrievedData: false,
      }
      
    },
    
  
 mounted() {
    this.getCD();
  },
  methods: {
   getCD: async function  () {
      this.retrievedData = false;
      try {
        let data = await fetch(
          "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
        )
        let object=await data.json
        let birth= object.filter((dog)=>dog.animalbirth)
           this.getCD.datasets[0].data.push(dog.length);
      }
      
      catch (error) {
        console.log(error);
      }
            this.retrievedData = true;
  }
    
  }
  }
  </script>