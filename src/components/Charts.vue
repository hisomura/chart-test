<template>
  <div class="small">
    <div class="chart-wrapper">
      <LineChart
        :chart-data="dataCollection"
        :initMin="min"
        :initMax="max"
      ></LineChart>
    </div>
    <button @click="goLeft()">goLeft</button>
    <button @click="fillData()">Randomize</button>
    <button @click="goRight()">goRight</button>
  </div>
</template>

<script>
import LineChart from './chart/LineChart.vue'
import { addDays, addHours } from 'date-fns'
const getRandomInt = () => Math.floor(Math.random() * (50 - 5 + 1)) + 5
const sliceAndFill = (arr, offset, size) => {
  const emptySize = size - (arr.length - arr.length)
  return arr
    .slice(offset, offset + size)
    .concat(Array.from({ length: emptySize }))
}
export default {
  components: {
    LineChart
  },
  data() {
    return {
      totalLabels: [],
      totalData: [],
      offset: 0,
      plotNum: 100,
      min: addDays(new Date(), -500),
      max: addDays(new Date(), 500)
    }
  },
  computed: {
    dataCollection() {
      return {
        labels: this.totalLabels,
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
    goLeft() {
      this.min = addDays(this.min, -50)
      this.max = addDays(this.max, -50)
    },
    goRight() {
      this.min = addDays(this.min, 50)
      this.max = addDays(this.max, 50)
    },
    fillData() {
      this.totalLabels = Array.from({ length: 1000 }, (v, i) => {
        return addDays(new Date(), i - 500)
      })
      this.totalData = Array.from({ length: 1000 }, () => getRandomInt())
    }
  }
}
</script>

<style scoped>
/*.chart-wrapper {*/
/*  width: 1000px;*/
/*}*/
</style>
