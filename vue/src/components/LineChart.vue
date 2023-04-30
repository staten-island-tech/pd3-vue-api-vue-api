<template>
  <h1 class="title">Years</h1>
  <Line v-if="loaded" :data="chartData" :options="chartOptions" />
</template>

<script>
import { Line } from 'vue-chartjs'
import { Chart as ChartJS, LineElement, Tooltip, Legend } from 'chart.js'
ChartJS.register(LineElement, Tooltip, Legend)
export default {
  name: 'LineChart',
  components: { Line },
  data() {
    return {
      loaded: false,
      chartData: {
        labels: [2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022],
        datasets: [
          {
            label: '311 Calls from every year',
            data: [],
            fill: false,
            borderColor: 'rgb(75, 192, 192)',
            tension: 0.1
          }
        ]
      },
      chartOptions: {
        responsive: true
      }
    }
  },
  async mounted() {
    this.loaded = false
    try {
      const response = await fetch(
        'https://data.cityofnewyork.us/resource/erm2-nwe9.json?$select=date_trunc_y(created_date)%20AS%20year,%20count(*)%20AS%20count&$group=year&$order=year'
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

<style lang="scss" scoped></style>
