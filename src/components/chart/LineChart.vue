<script>
import { Line, mixins } from 'vue-chartjs'

export default {
  extends: Line,
  mixins: [mixins.reactiveProp],
  // props: ["options"],
  data() {
    return {
      options: {
        responsive: true,
        animation: false,
        maintainAspectRatio: false,
        aspectRatio: 1,
        legend: false,
        scales: {
          xAxes: [
            {
              type: 'time',
              display: true
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
    this.renderChart(this.chartData, this.options)
  }
}
</script>
