<template>
  <div class="plot-wrapper">
    <scatter-chart :chart-data="dataCollection"></scatter-chart>
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
      pointCoordinates: Array,
      predictedPointCoordinates: Object
    },
    computed: {
      dataCollection () {
        return {
          labels: ['X', 'Y'],
          datasets: [
            {
              label: 'Predicted Linear Regression Line',
              borderColor: '#41B883',
              borderWidth: 5,
              data: [
                {x: this.minX, y: this.minY},
                {x: this.maxX, y: this.maxY}
              ],
              fill: false,
              showLine: true,
              pointRadius: 0
            },
            {
              label: 'Data Points (Xs and Ys)',
              backgroundColor: '#35495E',
              data: this.pointCoordinates,
              showLine: false,
              pointRadius: 10
            },
            {
              label: 'Predicted Point',
              backgroundColor: '#41B883',
              borderColor: '#35495E',
              borderWidth: 3,
              data: [this.predictedPointCoordinates],
              showLine: false,
              pointRadius: 15
            }
          ]
        }
      }
    },
  }
</script>

<style>
  .plot-wrapper {
    max-width: 600px;
    margin: 2em auto;
  }
</style>
