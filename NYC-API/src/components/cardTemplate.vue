<script>
export default {
  name: "cardTemplate",
  props: {
    breed: String,
  },
  methods: {
    addToChart: async function (breed) {
      retrievedData = false;
      try {
        let data = await fetch(
          "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
        );
        let object = await data.json();
        let array = object.filter((dog) => dog.breed === breed);
        this.chartData.labels.push(breed);
        this.chartData.datasets[0].data.push(array.length);
        retrievedData = true;
        console.log(data);
      } catch (e) {
        console.error(e);
        console.log(e);
      }
    },
  },
};
</script>
<template>
  <div class="card">
    <h2 class="breedlabel">{{ breed }}</h2>
    <button class="button" v-on="addToChart">Add to chart</button>
  </div>
</template>
