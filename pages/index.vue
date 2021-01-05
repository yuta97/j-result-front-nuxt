<template>
  <div class="container">
    <div>
      <LineChart 
      v-if="loaded"
      :results="results"/>
      {{results}}
    </div>
  </div>
</template>

<script>
import LineChart from '@/components/LineChart.vue'
import axios from 'axios';
export default {
  components: {
    LineChart
  },
  data: () => ({
    loaded: false,
    results: []
  }),
  async mounted () {
    this.loaded = false
    axios.get('https://p8zs9hb2kf.execute-api.ap-northeast-1.amazonaws.com/dev?year=2019&team_name=%E6%9C%AD%E5%B9%8C')
    .then(response => {
      this.loaded = true
      let ar = response.data.map(sale=>sale.result)
      let sum = 0
      for(let i = 0; i < ar.length; i++) {
        sum += ar[i]
        // console.log(sum)
        this.results.push(sum)
      }
      // this.results = response.data.map(sale=>sale.result);
    });
    // console.log(this.results)
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
