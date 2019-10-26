<template>
  <div class="small">
    <scatter-chart :chart-data="datacollection"></scatter-chart>
    <button @click="fillData()">Randomize</button>
  </div>
</template>

<script>
  import ScatterChart from './ScatterChart.js'

  export default {
    components: {
      ScatterChart
    },
    props: {
      minX: Number,
      maxX: Number,
      minY: Number,
      maxY: Number,

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
              data: [{x:0, y:6}, {x:4, y:9}],
              fill: false,
              showLine: true,
              pointRadius: 0
            }, {
              label: 'Data Points (Xs and Ys)',
              backgroundColor: '#35495E',
              data: [{x:1, y:5}, {x:2, y:4}],
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
