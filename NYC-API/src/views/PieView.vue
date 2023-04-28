<script>
import PieChart from "../components/Charts/PieChart.vue";
export default {
  name: "PieChart",
  components: {
    PieChart,
  },
  data() {
    return {
      chartData: {
        labels: ["male", "female"],
        datasets: [{ data: [2, 3] }],
      },
      chartOptions: {
        responsive: true,
      },
    };
  },
  methods: {
    getData: async function () {
      let data = await fetch(
        "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
      );
      let object = await data.json();
      let male = object.filter((dog) => (dog.animalgender = "M"));
      this.chartData.datasets[0].data.push(male.length);
      let female = object.filter((dog) => (dog.animalgender = "F"));
      this.chartData.datasets[0].data.push(female.length);
    },
  },
};
</script>

<template>
  <div class="PieView">
    <button class="test" v-on:click="getData">eeeeeeeee</button>
  </div>
</template>

<style>
.test {
  font-size: 100px;
}
</style>
