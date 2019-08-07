<template>
  <div id="app">
    <chart/>
    <advanced-chart/>
    <box-plot/>
    <annotations />
  </div>
</template>

<script>
import Chart from './components/Chart.vue'
import AdvancedChart from './components/AdvancedChart.vue'
import BoxPlot from './components/BoxPlot.vue'
import Annotations from './components/Annotations.vue'

export default {
  name: 'app',
  components: {
    Chart,
    AdvancedChart,
    BoxPlot,
    Annotations,
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
