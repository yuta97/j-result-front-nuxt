<template>
  <div class="container">
    <div>
      <select type="number" name="year" v-model="year1">
        <option v-for="n in 4" v-bind:value="n + 2016">{{ n + 2016 }}年</option>
      </select>
      <select v-model="team1">
        <option v-for="team1 in teams" v-bind:value="team1">{{ team1 }}</option>
      </select>
      <button @click="getApi1" >検索1</button>
    </div>
    
    <div>
      <select type="number" name="year" v-model="year2">
        <option v-for="n in 4" v-bind:value="n + 2016">{{ n + 2016 }}年</option>
      </select>
      <select v-model="team2">
        <option v-for="team2 in teams" v-bind:value="team2">{{ team2 }}</option>
      </select>
      <button @click="getApi2" >検索2</button>
    </div>
    <div>
      <LineChart 
      v-if="loaded"
      :results1="results1" :year1="year1" :team1="team1"
      :results2="results2" :year2="year2" :team2="team2"/>
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
    teams: ['札幌','仙台','鹿島','浦和','柏','FC東京','川崎Ｆ','横浜FM','横浜FC','湘南','清水','名古屋','Ｇ大阪','Ｃ大阪','神戸','広島','鳥栖','大分','松本','磐田','長崎','大宮'],
    year1: 2020,
    team1: '札幌',
    results1: [],
    year2: 2020,
    team2: '札幌',
    results2: []
  }),
  methods: {
    async getApi1() {
      console.log('getApi1')
      this.results1 = []
      this.loaded = false
      axios.get(`https://p8zs9hb2kf.execute-api.ap-northeast-1.amazonaws.com/dev?year=${this.year1}&team_name=${this.team1}`)
      .then(response => {
        this.loaded = true
        console.log(response)
        let ar = response.data.map(sale=>sale.result)
        let sum = 0
        for(let i = 0; i < ar.length; i++) {
          sum += ar[i]
          this.results1.push(sum)
          // console.log(sum)
        }
      })
    },
    async getApi2() {
      console.log('getApi2')
      this.results2 = []
      this.loaded = false
      axios.get(`https://p8zs9hb2kf.execute-api.ap-northeast-1.amazonaws.com/dev?year=${this.year2}&team_name=${this.team2}`)
      .then(response => {
        this.loaded = true
        console.log(response)
        let ar = response.data.map(sale=>sale.result)
        let sum = 0
        for(let i = 0; i < ar.length; i++) {
          sum += ar[i]
          this.results2.push(sum)
          // console.log(sum)
        }
      })
    }
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
