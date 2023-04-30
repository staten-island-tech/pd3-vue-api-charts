<template>
    <Bar
      v-if="retrievedData"
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
        datasets: [{ data: [] }],
      },
      chartOptions: {
        responsive: true,
        backgroundColor: ["#000fff"],
      },
      retrievedData: false,
    };
  },
  mounted() {
    this.getChartData();
  },
  methods: {
    getChartData: async function () {
      this.retrievedData = false;
      let years = [];
      let time = [];
      try {
        let data = await fetch(
          "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
        );
        let object = await data.json();
        let allYears = [];
        object.forEach((dog) => {
          allYears.push(dog.animalbirth);
        });
        years = new Set(allYears);
        years.forEach((year) => {
          time.push(year);
        });
        let finalYears = time.sort();
        this.chartData.labels = finalYears;
        finalYears.forEach((year) => {
          let count = this.filter(object, year);
          this.chartData.datasets[0].data.push(count.length);
        });
        this.retrievedData = true;
      } catch (error) {
        console.log(error);
      }
    },
    filter: function (object, year) {
      return object.filter((dog) => dog.animalbirth === year);
    },
  },
};
</script>
