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
        datasets: [{ label: ["birth years"], data: [] }],
      },
      chartOptions: {
        responsive: true,
        backgroundColor: ["#00BD7E"],
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
  <div class="main">
    <div class="heading" data-aos="fade-down" data-aos-duration="1500">
      <h1>Number of dogs born in each year:</h1>
    </div>
    <div class="barChart" data-aos="fade-up" data-aos-duration="1500">
      <BarChart
        class="bar"
        v-if="retrievedData"
        :chartData="chartData"
        :chartOptions="chartOptions"
      />
    </div>
    <div class="text" data-aos="fade-up-left" data-aos-duration="1500">
      <p>
        Here, we can see how many dogs were born in a timespan of 15 years
        consecutively from 2000-2014.
      </p>
    </div>
  </div>
</template>

<style scoped>
.main {
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: center;
  display: flex;
  width: 100vw;
}
.text {
  width: 10vw;
  height: 50vh;
  position: relative;
  top: 10vw;
  font-size: 20px;
}
.bar {
  width: 70vw;
  display: flex;
  flex-wrap: wrap;
}

.barChart {
  width: 75vw;
}

.heading {
  font-size: 20px;
  text-align: center;
  margin: 40px 0px;
}
</style>
