<script>
import { Line } from 'vue-chartjs'
export default {
  extends: Line,
  data(){
    return {
        chartdata: {
            labels: [1,2,3],
            datasets: [
                {
                lineTension: 0, 
                // 直線的な推移
                label: ['勝ち点推移'],
                backgroundColor: '#f87979',
                data: [0, 30,100]
                }
            ]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false
        }
    }
  },
  mounted () {
    this.renderChart(this.chartdata, this.options)
  }
}
</script>