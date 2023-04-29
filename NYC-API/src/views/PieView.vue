<script>
import PieChart from "../components/Charts/PieChart.vue";
export default {
  name: "PieChartView",
  components: {
    PieChart,
  },
  data() {
    return {
      chartData: {
        labels: ["Male", "Female"],
        datasets: [{ data: [] }],
      },
      chartOptions: {
        responsive: true,
        backgroundColor: ["0000FF", "AA336A"],
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
      try {
        let data = await fetch(
          "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
        );
        let object = await data.json();
        let male = object.filter((dog) => dog.animalgender === "M");
        this.chartData.datasets[0].data.push(male.length);
        let female = object.filter((dog) => dog.animalgender === "F");
        this.chartData.datasets[0].data.push(female.length);
        this.retrievedData = true;
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<template>
  <div class="pie">
    <button class="test" v-on:click="getChartData">eeeeeeeee</button>
    <PieChart
      v-if="retrievedData"
      :chartData="chartData"
      :chartOptions="chartOptions"
    />
  </div>
</template>

<style>
.test {
  font-size: 100px;
}
</style>
