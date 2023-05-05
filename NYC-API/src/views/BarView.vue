<script>
import BarChart from "../components/Charts/BarChart.vue";
export default {
  name: "BarChartView",
  components: {
    BarChart,
  },
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

<template>
  <div class="bar">
    <BarChart
      v-if="retrievedData"
      :chartData="chartData"
      :chartOptions="chartOptions"
    />
  </div>
</template>
