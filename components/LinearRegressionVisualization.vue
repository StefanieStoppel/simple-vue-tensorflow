<template>
  <div class="small">
    <line-chart :chart-data="datacollection"></line-chart>
    <button @click="fillData()">Randomize</button>
  </div>
</template>

<script>
  import LineChart from './LineChart.js'

  export default {
    components: {
      LineChart
    },
    data () {
      return {
        datacollection: null
      }
    },
    mounted () {
      this.fillData()
    },
    methods: {
      fillData () {
        this.datacollection = {
          labels: ['X', 'Y'],
          datasets: [
            {
              label: 'Predicted Linear Regression Line',
              borderColor: '#41B883',
              borderWidth: 5,
              data: [this.getRandomInt(), this.getRandomInt()],
              fill: false,
              pointRadius: 0
            }, {
              label: 'Data Points (Xs and Ys)',
              backgroundColor: '#35495E',
              data: [this.getRandomInt(), this.getRandomInt()],
              showLine: false,
              pointRadius: 10
            }
          ]
        }
      },
      getRandomInt () {
        return Math.floor(Math.random() * (50 - 5 + 1)) + 5
      }
    }
  }
</script>

<style>
  .small {
    max-width: 600px;
    margin:  150px auto;
  }
</style>
