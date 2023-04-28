<script setup>
import BarChart from "../components/Charts/BarChart.vue";
import { ref, onMounted } from "vue";
const dogs = ref("");
async function getData() {
  this.retrievedData = false;
  try {
    let data = await fetch(
      "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
    );
    console.log(data);
    let object = await data.json();
    console.log(object);
    dogs.value = object;
    console.log(dogs);
    this.retrievedData = true;
  } catch (error) {
    console.log(error);
  }
}
onMounted(() => {
  getData();
});
</script>

<template>
  <div class="BarView">
    <BarChart v-if="retrievedData" :chartData="dogs" />
    <h1>hi</h1>
  </div>
</template>
