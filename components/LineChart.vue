<script>
import { Line } from 'vue-chartjs'


export default {
  extends: Line,
  props: ['results1','year1','team1','results2','year2','team2'],
  data(){
    return {
        chartdata: {
            labels: Array.from({ length: 34 }, (_, i) => i + 1),
            datasets: [
                {
                lineTension: 0, 
                // 直線的な推移
                label: [`${this.year1}年の${this.team1}の勝ち点`],
                // backgroundColor: '#f87979',
                borderColor: "rgba(255,0,0,1)",
                backgroundColor: "rgba(0,0,0,0)",
                data: this.results1
                },
                {
                lineTension: 0, 
                // 直線的な推移
                label: [`${this.year2}年の${this.team2}の勝ち点`],
                // backgroundColor: '#f87979',
                borderColor: "rgba(0,0,255,1)",
                backgroundColor: "rgba(0,0,0,0)",
                data: this.results2
                }
            ]
        },
        options: {
            responsive: true,
            maintainAspectRatio: false
        },
        records: []
    }
  },
  mounted () {
    this.renderChart(this.chartdata, this.options)
    // console.log(this.results1)
  }
}
</script>