<template>
  <div>
    <button @click="addAnnotation">Add Annotation</button>
    <highcharts ref="highchart" :options="chartOptions" />
  </div>
</template>

<script>
import Highcharts from "highcharts";
import highchartsMore from "highcharts/highcharts-more";
import annotations from "highcharts/modules/annotations";
import { Chart } from "highcharts-vue";
highchartsMore(Highcharts);
annotations(Highcharts);
export default {
  components: {
    highcharts: Chart
  },
  methods: {
    addAnnotation() {
      this.chartOptions.annotations.push({
        labels: [
          {
            point: {
              x: 0,
              y: 0
            },
            text: "Custom 1"
          },
          {
            point: {
              x: 0,
              y: 10
            },
            text: "Custom 2",
            backgroundColor: "white"
          }
        ]
      });
      // this.$refs.highchart.chart.redraw()
    }
  },
  data() {
    return {
      chartOptions: {
        xAxis: {
          categories: [
            "Jan",
            "Feb",
            "Mar",
            "Apr",
            "May",
            "Jun",
            "Jul",
            "Aug",
            "Sep",
            "Oct",
            "Nov",
            "Dec"
          ]
        },

        title: {
          text: "Highcharts Annotations"
        },

        series: [
          {
            data: [
              { y: 29.9, id: "min" },
              71.5,
              106.4,
              129.2,
              144.0,
              176.0,
              135.6,
              148.5,
              { y: 216.4, id: "max" },
              194.1,
              95.6,
              54.4
            ]
          }
        ],
        annotations: [
          {
            labels: [
              {
                point: "max",
                text: "Max"
              },
              {
                point: "min",
                text: "Min",
                backgroundColor: "white"
              }
            ]
          }
        ]
      }
    };
  }
};
</script>

<style>
</style>
