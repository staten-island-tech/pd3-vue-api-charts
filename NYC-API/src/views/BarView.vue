<script setup>
import BarChart from "../components/Charts/BarChart.vue";
import { ref, onMounted } from "vue";
const dogs = ref("");
async function getData() {
  let data = await fetch(
    "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
  );
  let object = data.json();
  dogs.value = object.results;
  this.retrievedData = true;
}
onMounted(() => {
  getData();
});
</script>

<template>
  <div class="bar">
    <BarChart :chartData="dogs" />
    <h1>hi</h1>
  </div>
</template>
