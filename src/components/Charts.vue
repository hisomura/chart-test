<template>
  <div class="small">
    <div class="chart-wrapper">
      <LineChart :chart-data="dataCollection"></LineChart>
    </div>
    <button @click="fillData()">Randomize</button>
  </div>
</template>

<script>
import LineChart from './chart/LineChart.vue'
import { addDays } from 'date-fns'
const getRandomInt = () => Math.floor(Math.random() * (50 - 5 + 1)) + 5
export default {
  components: {
    LineChart
  },
  data() {
    return {
      dataCollection: null
    }
  },
  mounted() {
    this.fillData()
  },
  methods: {
    fillData() {
      const dataLength = 300
      const labels = Array.from({ length: dataLength }, (v, i) => {
        return addDays(new Date(), i)
      })
      const data = Array.from({ length: dataLength }, (v, i) => {
        return getRandomInt()
      })

      this.dataCollection = {
        labels: labels.slice(100, 200),
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979',
            data: data.slice(100, 200)
          }
        ]
      }
    }
  }
}
</script>

<style scoped>
/*.chart-wrapper {*/
/*  width: 1000px;*/
/*}*/
</style>
