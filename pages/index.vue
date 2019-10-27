<template>
  <section class="container">
    <div>
      <app-logo/>
      <h1 class="title">
        simple-vue-tensorflow + Chart.js
      </h1>
      <h2 class="subtitle">
        Nuxt.js project
      </h2>
      <tensorflow-example/>
    </div>
  </section>
</template>

<script>
import AppLogo from '~/components/AppLogo.vue'
import TensorflowExample from '~/components/TensorflowExample.vue'

export default {
  components: {
    AppLogo,
    TensorflowExample
  }
}

</script>

<style>

.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 36px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 28px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
