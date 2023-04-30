<template>
  <h1 class="title">Boroughs</h1>
  <Doughnut v-if="loaded" :data="chartData" :options="chartOptions" />
</template>

<script>
import { Doughnut } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
} from 'chart.js'
ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)
export default {
  name: 'DoughnutChart',
  components: { Doughnut },
  data: () => ({
    loaded: false,
    chartData: {
      labels: ['Brooklyn', 'Bronx', 'Staten Island', 'Manhattan', 'Queens', 'Unspecified'],
      datasets: [
        {
          label: 'Boroughs',
          data: [],
          backgroundColor: ['#333ED4', '#2FA236', '#A0D636', '#EEDE04', '#F76915', '#FD0100'],
          hoverOffset: 4
        }
      ]
    },
    chartOptions: {
      responsive: true,
      maintainAspectRatio: true
    }
  }),
  async mounted() {
    this.loaded = false
    try {
      const { boroughs } = await fetch(
        'https://data.cityofnewyork.us/resource/erm2-nwe9.json?$where=created_date%3E=%272010-01-01T00:00:00.000%27&$group=borough&$select=borough,count(*)'
      )
      this.chartdata = boroughs
      this.loaded = true
    } catch (e) {
      console.error(e)
    }
  }
}
</script>

<style lang="scss" scoped></style>
