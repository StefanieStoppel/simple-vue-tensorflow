<template>
  <div class="row">
    <LinearRegressionVisualization
      :min-x="minXValue"
      :min-y="minYValue"
      :max-x="maxXValue"
      :max-y="maxYValue"
      :point-coordinates="pointCoordinates"
      :predicted-point-coordinates="predictedPointCoordinates">
    </LinearRegressionVisualization>

    <div class="train-controls col-sm-8">
      <h2 class="section col-sm-1">Training Data (x,y) pairs</h2>
      <div class="field-label">X</div><div class="field-label">Y</div>

      <div v-for="(item, index) in xValues" v-bind:key="index">
        <div>

          <div class="col-sm-1">
            <input class="field field-x" v-model="xValues[index]" type="number">
            <input class="field field-y" v-model="yValues[index]" type="number">
          </div>
      </div>
      </div>

      <button class="button-add-example button--green" @click.stop="addItem">+</button>
      <button class="button-train button--green" @click="train">Train</button>
    </div>

    <div class="predict-controls">
      <h2 class="section col-sm-1">Predicting</h2>
      <input class="field element" v-model="valueToPredict" type="number" placeholder="Enter an integer number"><br>
      <div class="element" v-if="predictedValue !== null">{{predictedValue}}</div>
      <div class="element" v-if="!trained">Click on train!</div>
      <button class="element button--green" v-on:click="predict" :disabled="!trained">Predict</button>
    </div>
  </div>
</template>

<script>
import * as tf from '@tensorflow/tfjs';
import LinearRegressionVisualization from "./LinearRegressionVisualization";

export default {
  components: {LinearRegressionVisualization},
  data() {
    return {
      model: null,
      minYValue: null,
      maxYValue: null,
      trained: false,
      xValues: [1,2,4,8],
      yValues: [1,3,5,45],
      predictedValue: null,
      valueToPredict: null
    }
  },
  methods: {
    addItem() {
      this.xValues.push(0);
      this.yValues.push(0);
    },
    train() {
      // Define a model for linear regression.
      this.model = tf.sequential();
      this.model.add(tf.layers.dense({units: 1, inputShape: [1]}));

      // Prepare the model for training: Specify the loss and the optimizer.
      this.model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

      const xs = tf.tensor2d(this.xValues, [this.xValues.length, 1]);
      const ys = tf.tensor2d(this.yValues, [this.yValues.length, 1]);

      // Train the model using the data.
      this.model.fit(xs, ys, {epochs: 50}).then(() => {
        this.trained = true;
        this.predictedValue = 'Ready for making predictions';
        this.minYValue = this.model.predict(tf.tensor2d([this.minXValue], [1, 1])).get(0, 0);
        this.maxYValue = this.model.predict(tf.tensor2d([this.maxXValue], [1, 1])).get(0, 0);
      });
    },
    predict() {
      // Use the model to do inference on a data point the model hasn't seen before:
      this.predictedValue = this.model.predict(tf.tensor2d([this.valueToPredict], [1, 1])).get(0, 0);
    }
  },
  computed: {
    minXValue() {
      return Math.min(...this.xValues)
    },
    maxXValue() {
      return Math.max(...this.xValues)
    },
    pointCoordinates() {
      return this.xValues.map((x, index) => {
        return {x, y: this.yValues[index]}
      })
    },
    predictedPointCoordinates() {
      return {x: parseInt(this.valueToPredict), y: parseInt(this.predictedValue)}
    }
  }
}
</script>

<style>
.field, .field-label {
  height: 30px;
  padding: 0px 15px;
  float: left;
  width: 50%;
}

.field {
  border-radius: 0px 5px 5px 0px;
  border: 1px solid #eee;
  margin-bottom: 15px;
  height: 40px;
}

.col-sm-1:after {
    content: "";
    display: table;
    clear: both;
}

.section, .field-label {
  text-align: left;
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  font-weight: 100;
}

.field-label {
  font-weight: 700;
}

.button-add-example {
  width: 100%;
  margin-bottom: 10px;
}

.button-train {
  width: 100%;
}

.predict-controls {
  padding-top: 30px;
  padding-bottom: 30px;
}

.predict-controls .element {
  width: 50%;
  display: block;
}

button {
  margin-top: 10px;
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  font-weight: 700;
}

</style>
