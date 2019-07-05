<template>
  <div class="small">
    <div class="chart-wrapper">
      <LineChart :chart-data="dataCollection"></LineChart>
    </div>
    <button @click="fillData()">Randomize</button>
    <button @click="goRight()">goRight</button>
  </div>
</template>

<script>
import LineChart from './chart/LineChart.vue'
import { addDays, addHours } from 'date-fns'
const getRandomInt = () => Math.floor(Math.random() * (50 - 5 + 1)) + 5
export default {
  components: {
    LineChart
  },
  data() {
    return {
      totalLabels: [],
      totalData: [],
      offset: 100,
      plotNum: 100
    }
  },
  computed: {
    dataCollection() {
      return {
        labels: this.totalLabels.slice(this.offset, this.offset + this.plotNum),
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979',
            data: this.totalData
          }
        ]
      }
    }
  },
  mounted() {
    this.fillData()
  },
  methods: {
    goRight() {
      this.offset += 50
    },
    fillData() {
      const dateLength = 300
      this.totalLabels = Array.from({ length: dateLength }, (v, i) => {
        return addDays(new Date(), i)
      })
      const startDate = addDays(new Date(), 100)
      this.totalData = Array.from({ length: 400 }, (v, i) => {
        return {
          x: addHours(addDays(startDate, i / 4), (i % 4) * 6),
          y: getRandomInt()
        }
      })
      this.offset = 100
    }
  }
}
</script>

<style scoped>
/*.chart-wrapper {*/
/*  width: 1000px;*/
/*}*/
</style>
