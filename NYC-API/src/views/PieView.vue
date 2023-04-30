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
        labels: [],
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
    clearChartData: function () {
      this.retrievedData = false;
      this.chartData.datasets[0].data.length = 0;
      this.chartData.labels.length = 0;
      console.log(this.chartData.datasets[0].data.length);
      console.log(this.chartData.labels.length);
    },
    getChartData: async function () {
      this.retrievedData = false;
      try {
        let data = await fetch(
          "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
        );
        let object = await data.json();
        let male = object.filter((dog) => dog.animalgender === "M");
        this.chartData.labels.push("Male");
        this.chartData.datasets[0].data.push(male.length);
        let female = object.filter((dog) => dog.animalgender === "F");
        this.chartData.labels.push("Female");
        this.chartData.datasets[0].data.push(female.length);
        this.retrievedData = true;
      } catch (error) {
        console.log(error);
      }
    },
    getLiscenseData: async function () {
      this.retrievedData = false;
      let dates = [];
      let labels = [];
      try {
        let data = await fetch(
          "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
        );
        let object = await data.json();
        object.forEach((dog) => {
          let year = dog.licenseissueddate.substring(0, 7);
          dates.push(year);
        });
        let noDupes = new Set(dates);
        noDupes.forEach((month) => {
          labels.push(month);
        });
        let ordered = labels.sort();
        this.filter(september, 0);
        this.filter(october, 1);
        this.filter(november, 2);
        this.filter(december, 3);
        this.chartData.labels = ordered;
        this.retrievedData = true;
      } catch (error) {
        console.log(error);
      }
    },
    filter: function (month, index) {
      let month = object.filter(
        (dog) => dog.licenseissueddate.substring(0, 7) === ordered[index]
      );
      this.chartData.datasets[0].data.push(month.length);
    },
    years: function () {
      this.clearChartData();
      this.getLiscenseData();
    },
    gender: function () {
      this.clearChartData();
      this.getChartData();
    },
  },
};
</script>

<template>
  <div class="pie">
    <button class="test" v-on:click="years">go</button>
    <button class="button" v-on:click="gender">go</button>
    <PieChart
      v-if="retrievedData"
      :chartData="chartData"
      :chartOptions="chartOptions"
    />
  </div>
</template>

<style>
.test {
  font-size: 20px;
}
</style>
