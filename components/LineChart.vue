<script>
import { Line } from 'vue-chartjs'


export default {
  extends: Line,
  props: ['results'],
  data(){
    return {
        chartdata: {
            labels: Array.from({ length: 34 }, (_, i) => i + 1),
            datasets: [
                {
                lineTension: 0, 
                // 直線的な推移
                label: ['勝ち点推移'],
                backgroundColor: '#f87979',
                data: this.results
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
    console.log(this.results)
  },
  // mounted(){
  //   axios.get('https://p8zs9hb2kf.execute-api.ap-northeast-1.amazonaws.com/dev?year=2019&team_name=%E6%9C%AD%E5%B9%8C')
  //         .then(response => this.records = response.data);
  //   console.log(this.records)
  // }
}
</script>