<script>
import { Line, mixins } from 'vue-chartjs'

export default {
  extends: Line,
  mixins: [mixins.reactiveProp],
  props: {
    min: {
      type: Date,
      required: true
    },
    max: {
      type: Date,
      required: true
    }
  },
  computed: {},
  watch: {
    min(newVal, oldVal) {
      this.renderChart(this.chartData, this.options())
    },
    max(newVal, oldVal) {
      this.renderChart(this.chartData, this.options())
    }
  },
  methods: {
    options() {
      return {
        responsive: true,
        animation: false,
        maintainAspectRatio: false,
        aspectRatio: 1,
        legend: false,
        scales: {
          xAxes: [
            {
              type: 'time',
              distribution: 'linear',
              display: true,
              time: {
                max: this.max,
                min: this.min
              }
            }
          ],
          yAxes: [
            {
              ticks: {
                max: 50,
                min: -1
              }
            }
          ]
        }
      }
    }
  },
  mounted() {
    this.renderChart(this.chartData, this.options())
  }
}
</script>
