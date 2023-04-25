<script setup>
import TheWelcome from '../components/TheWelcome.vue'
import BarChart from '../components/Chart/ChartTemplate.vue'

</script>


  <template>
  <BarChart />
</template>

<script>
import BarChart from 'path/to/component/BarChart'

export default {
  name: 'App',
  components: { BarChart }
}
</script>
  <main>
    <TheWelcome />
  </main>
</template>
