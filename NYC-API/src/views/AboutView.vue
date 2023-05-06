<script></script>

<template>
  <div class="about">
    <h1
      class="descriptionTitle"
      data-aos="zoom-in-down"
      data-aos-duration="3000"
    >
      About the devs:
    </h1>
    <p data-aos="zoom-in-up" data-aos-duration="3000">
      This Vue chart project was made by Leo Dwi and Dominic Lin. Inside, you
      will find a bar chart containing the amount of dogs born in a specific
      year from a dataset consisting of the years 2000 to 2014. You will also
      find a pie chart that sorts dogs by gender with a sample size of 1000, as
      well as the licenses that were issued from september 2014 to december
      2014.
    </p>
  </div>
</template>

<style scoped>
.about {
  text-align: center;
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: center;
}
.descriptionTitle {
  margin: 50px, 0px;
  font-size: 40px;
}
p {
  font-size: 20px;
  width: 55vw;
  margin: auto;
}

h1 {
  margin: 40px;
}
</style>
