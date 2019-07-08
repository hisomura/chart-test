<script>
import { Line, mixins } from 'vue-chartjs'
import { addDays, addHours } from 'date-fns'

export default {
  extends: Line,
  render(createElement) {
    return createElement(
      'div',
      {
        style: this.styles,
        class: this.cssClasses
      },
      [
        createElement('canvas', {
          attrs: {
            id: this.chartId,
            width: this.width,
            height: this.height,
            draggable: true
          },
          ref: 'canvas'
        }),
        createElement('span', {
          style: {
            position: 'absolute',
            display: 'block',
            top: 0,
            left: 0,
            width: 0,
            height: 0
          },
          ref: 'dragImg'
        })
      ]
    )
  },
  mixins: [mixins.reactiveProp],
  props: {
    initMin: {
      type: Date,
      required: true
    },
    initMax: {
      type: Date,
      required: true
    }
  },
  data() {
    return {
      min: this.initMin,
      max: this.initMax
    }
  },
  computed: {},
  watch: {},
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
    const self = this
    let prevX = undefined
    this.renderChart(this.chartData, this.options())
    this.$refs.canvas.addEventListener(
      'dragstart',
      function(event) {
        event.dataTransfer.effectAllowed = 'none'
        // https://stackoverflow.com/questions/7680285/how-do-you-turn-off-setdragimage
        event.dataTransfer.setDragImage(self.$refs.dragImg, 0, 0)
        prevX = event.offsetX
      },
      false
    )
    this.$refs.canvas.addEventListener(
      'dragover',
      function(event) {
        if (event.pageX % 10 === 0) {
          const diff = event.pageX - prevX
          prevX = event.pageX
          self.min = addDays(self.min, -diff)
          self.max = addDays(self.max, -diff)
          self.renderChart(self.chartData, self.options())
        }
      },
      false
    )
    this.$refs.canvas.addEventListener(
      'dragend',
      function(event) {
        prevX = undefined
      },
      false
    )
  }
}
</script>
