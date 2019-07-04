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
import { addDays } from 'date-fns'
const getRandomInt = () => Math.floor(Math.random() * (50 - 5 + 1)) + 5
export default {
  components: {
    LineChart
  },
  data() {
    return {
      totalLabels: [],
      totalData: [],
      offset: 0,
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
            data: this.totalData.slice(this.offset, this.offset + this.plotNum)
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
      this.offset += 50;
    },
    fillData() {
      const dataLength = 300
      this.totalLabels = Array.from({ length: dataLength }, (v, i) => {
        return addDays(new Date(), i)
      })
      this.totalData = Array.from({ length: dataLength }, (v, i) => {
        return getRandomInt()
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
