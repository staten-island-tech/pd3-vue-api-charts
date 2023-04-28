<script>
import PieChart from "../components/Charts/PieChart.vue";
export default {
  components: {
    pieChart,
  },
  data() {
    return {
      chartData: {
        labels: [male, female],
        datasets: [2, 3],
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
    },
  },
};
</script>
