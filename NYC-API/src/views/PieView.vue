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
        backgroundColor: ["#0000FF", "#FF0000"],
      },
      retrievedData: false,
      gender: true,
      license: false,
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
      this.chartOptions.backgroundColor.length = 0;
      console.log(this.chartData.datasets[0].data.length);
      console.log(this.chartData.labels.length);
    },
    getChartData: async function () {
      this.license = false;
      this.gender = true;
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
        this.chartOptions.backgroundColor.push("#0000FF", "#FF0000");
        this.retrievedData = true;
      } catch (error) {
        console.log(error);
      }
    },
    getLiscenseData: async function () {
      this.gender = false;
      this.license = true;
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
        this.filter(ordered, object, 0);
        this.filter(ordered, object, 1);
        this.filter(ordered, object, 2);
        this.filter(ordered, object, 3);
        this.chartData.labels = ordered;
        this.chartOptions.backgroundColor.push(
          "#01FFFF",
          "#00ECFA",
          "#00CEF1",
          "#00B8EA"
        );
        this.retrievedData = true;
      } catch (error) {
        console.log(error);
      }
    },
    filter: function (ordered, object, index) {
      let month = object.filter(
        (dog) => dog.licenseissueddate.substring(0, 7) === ordered[index]
      );
      this.chartData.datasets[0].data.push(month.length);
    },
    month: function () {
      this.clearChartData();
      this.getLiscenseData();
    },
    genders: function () {
      this.clearChartData();
      this.getChartData();
    },
  },
};
</script>

<template>
  <div class="pie">
    <div class="title" data-aos="fade-down" data-aos-duration="1500">
      <h2 v-if="gender" class="title">Gender data out of 1000 sample size</h2>
      <h2 v-if="license" class="title">
        Months of license issued in 2014, sept-dec
      </h2>
    </div>
    <div class="main">
      <div class="buttons">
        <div
          class="genders button"
          data-aos="fade-down-left"
          data-aos-duration="1500"
        >
          <h3>sort by gender:</h3>
          <button class="button" v-on:click="genders">go</button>
        </div>
        <div
          class="license button"
          data-aos="fade-up-left"
          data-aos-duration="1500"
        >
          <h3>sort by license date: (months)</h3>
          <button class="button" v-on:click="month">go</button>
        </div>
      </div>
      <div class="chart" data-aos="fade-up" data-aos-duration="1500">
        <PieChart
          class="chart"
          v-if="retrievedData"
          :chartData="chartData"
          :chartOptions="chartOptions"
        />
      </div>
      <div class="info" data-aos="fade-right" data-aos-duration="1500">
        <div class="gender-data" v-if="gender">
          <ul>
            <li>
              Males consist of 544 which make up around 54.4% out of a 1000
              sample size.
            </li>
            <li>
              Females consist of 456 which make up around 45.6% out of a 1000
              sample size.
            </li>
          </ul>
        </div>
        <div class="license-data" v-if="license">
          <ul>
            <li>In the month of september 2014, 233 licenses were issued.</li>
            <li>In the month of october 2014,369 licenses were issued.</li>
            <li>In the month of november 2014, 262 licenses were issued.</li>
            <li>In the month of december 2014, 136 licenses were issued.</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
h2 {
  font-size: 50px;
}
.title {
  text-align: center;
  margin: 40px 0px;
}
.main {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row-reverse;
  justify-content: space-evenly;
}
.buttons {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: space-around;
}
.info {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: space-around;
  position: relative;
  left: -50px;
}
button {
  background-color: #13aa52;
  border: 1px solid #13aa52;
  border-radius: 4px;
  box-shadow: rgba(0, 0, 0, 0.1) 0 2px 4px 0;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  font-family: "Akzidenz Grotesk BQ Medium", -apple-system, BlinkMacSystemFont,
    sans-serif;
  font-size: 16px;
  font-weight: 400;
  outline: none;
  outline: 0;
  padding: 10px 50px;
  text-align: center;
  transform: translateY(0);
  transition: transform 150ms, box-shadow 150ms;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}
button:hover {
  box-shadow: rgba(0, 0, 0, 0.15) 0 3px 9px 0;
  transform: translateY(-2px);
}
</style>
