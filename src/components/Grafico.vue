<script>
import { Line, mixins } from 'vue-chartjs'
const { reactiveProp } = mixins

export default {
  extends: Line,
  mixins: [reactiveProp],
  name: 'Grafico',
  data () {
    return {
      options: {
        scales: {
          yAxes: [{
            ticks: {
              callback: function (value, index, values) {
                return `$ ${value}`
              }
            }
          }]
        }
      }
    }
  },
  mounted () {
    this.renderChart(this.chartData, this.options)
  }
}
</script>
