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
      },
      retrievedData: false,
    };
  },
  methods: {
    getData: async function () {
      this.retrievedData = false;
      console.log(this.retrievedData);
      try {
        let data = await fetch(
          "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
        );
        let object = await data.json();
        let male = object.filter((dog) => dog.animalgender === "M");
        this.chartData.datasets[0].data.push(male.length);
        this.chartData.labels.push("Male");
        let female = object.filter((dog) => dog.animalgender === "F");
        this.chartData.datasets[0].data.push(female.length);
        this.chartData.labels.push("Female");
        console.log(object);
        console.log(male);
        console.log(female);
        console.log(this.chartData.datasets);
        this.retrievedData = true;
        console.log(this.retrievedData);
      } catch (error) {
        console.error(error);
        console.log(error);
      }
    },

    async mounted() {
      retrievedData = false;
      try {
        let data = await fetch(
          "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
        );
        let object = await data.json();
        let male = object.filter((dog) => dog.animalgender === "M");
        this.chartData.datasets[0].data.push(male.length);
        let female = object.filter((dog) => dog.animalgender === "F");
        this.chartData.datasets[0].data.push(female.length);
        retrievedData = true;
        console.log(data);
        console.log(male);
      } catch (e) {
        console.error(e);
        console.log(e);
      }
    },
  },
};
</script>

<template>
  <div class="pie">
    <button class="test" v-on:click="getData">eeeeeeeee</button>
    <PieChart :chartData="chartData" v-if="retrievedData" />
  </div>
</template>

<style>
.test {
  font-size: 100px;
}
</style>
