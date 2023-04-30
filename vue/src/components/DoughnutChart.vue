<template>
  <h2 class="title">Boroughs</h2>
  <Doughnut v-if="loaded" :data="chartData" :options="chartOptions" />
</template>

<script>
import { Doughnut } from 'vue-chartjs'
import { Chart as ChartJS, ArcElement, Tooltip, Legend } from 'chart.js'

ChartJS.register(ArcElement, Tooltip, Legend)

export default {
  name: 'DoughnutChart',
  components: { Doughnut },
  data() {
    return {
      loaded: false,
      chartData: {
        labels: ['BRONX', 'BROOKLYN', 'MANHATTAN', 'QUEENS', 'STATEN ISLAND', 'Unspecified'],
        datasets: [
          {
            data: []
          }
        ]
      },
      chartOptions: {
        responsive: true,
        backgroundColor: ['#333ED4', '#2FA236', '#A0D636', '#EEDE04', '#F76915', '#FD0100']
      }
    }
  },
  async mounted() {
    this.loaded = false
    try {
      const response = await fetch(
        'https://data.cityofnewyork.us/resource/erm2-nwe9.json?$where=created_date%3E=%272010-01-01T00:00:00.000%27&$group=borough&$select=borough,count(*)'
      )
      const data = await response.json()
      for (let i = 0; i < data.length - 1; i++) {
        this.chartData.datasets[0].data.push(data[i].count)
      }

      this.loaded = true
    } catch (e) {
      console.error(e)
    }
    console.log(this.chartData)
  }
}
</script>

<style></style>
