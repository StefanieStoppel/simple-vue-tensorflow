<template>
  <div class="small">
    <scatter-chart :chart-data="dataCollection"></scatter-chart>
    <div>{{pointCoordinates}}</div>
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
      pointCoordinates: Array
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
            }, {
              label: 'Data Points (Xs and Ys)',
              backgroundColor: '#35495E',
              data: this.pointCoordinates, // stuff
              showLine: false,
              pointRadius: 10
            }
          ]
        }
      }
    },
  }
</script>

<style>
  .small {
    max-width: 600px;
    margin:  150px auto;
  }
</style>
