<template>
    <Bar
      id="my-chart-id"
      :options="chartOptions"
      :data="chartData"
    />
  </template>
  
  <script>
  import { Bar } from 'vue-chartjs'
  import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
import { onMounted} from 'vue'
  
  ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)
  

  export default {
    name: 'BarChart',
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
      
    }
    
  }
 onMounted() ;{
    this.getCD();
  }
  methods: {
    async function getCD () {
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
  
  </script>