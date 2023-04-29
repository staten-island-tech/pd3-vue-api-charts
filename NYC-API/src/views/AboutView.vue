<script>
import cardTemplate from "../components/cardTemplate.vue";
export default {
  components: { cardTemplate },
  data() {
    return {
      retrievedData: false,
    };
  },
  computed: {
    breeds: async function () {
      this.retrievedData = false;
      let breeds = [];
      try {
        let data = await fetch(
          "https://data.cityofnewyork.us/resource/nu7n-tubp.json"
        );
        let object = await data.json();
        object.forEach((dog) => {
          if (breeds.includes(dog.breedname)) {
            console.log("e");
          } else {
            breeds.push(dog.breedname);
          }
          this.retrievedData = true;
          return breeds;
        });
      } catch (e) {
        console.error(e);
        console.log(e);
      }
    },
  },
};
</script>

<template>
  <div class="about" v-if="retrievedData">
    <h1>This is an about page</h1>
    <cardTemplate
      v-for="dogs in breeds"
      v-bind:key="dogs"
      :breed="dogs.breed"
    />
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
