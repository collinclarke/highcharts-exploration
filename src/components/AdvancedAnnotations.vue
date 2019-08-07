<template>
  <div>
    <button @click="addAnnotation">Add Annotation</button>
    <highcharts :options="chartOptions" />
  </div>
</template>

<script>
import elevationData from './data.js'
import Highcharts from 'highcharts' 
import highchartsMore from 'highcharts/highcharts-more'
import annotations from 'highcharts/modules/annotations'
import { Chart } from 'highcharts-vue'
highchartsMore(Highcharts)
annotations(Highcharts)
export default {
  components: {
    highcharts: Chart
  },
  methods: {
    addAnnotation () {
      this.chartOptions.annotations[0].labels.push({
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 159,
                    y: 443
                },
                text: 'Saint-Claude'
            })
    }
  },
  data() {
    return {
      chartOptions: {
        // Data generated from http://www.bikeforums.net/professional-cycling-fans/1113087-2017-tour-de-france-gpx-tcx-files.html
        chart: {
          type: 'area',
          zoomType: 'x',
          panning: true,
          panKey: 'shift',
          scrollablePlotArea: {
              minWidth: 600
          }
        },

        accessibility: {
            description: 'An annotated line graph illustrates the 8th stage of the 2017 Tour de France cycling race from the start point in Dole to the finish line at Station des Rousses. Altitude is plotted on the Y-axis at increments of 500m and distance is plotted on the X-axis in increments of 25 kilometers. The line graph is interactive, and the user can trace the altitude level at every 100-meter point along the stage. The graph is shaded below the data line to visualize the mountainous altitudes encountered on the 187.5-kilometre stage. The three largest climbs are highlighted at Col de la Joux, Côte de Viry and the final 11.7-kilometer, 6.4% gradient climb to Montée de la Combe de Laisia Les Molunes which peaks at 1200 meters above sea level. The stage passes through the villages of Arbois, Montrond, Bonlieu, Chassal and Saint-Claude along the route.'
        },

        title: {
            text: '2017 Tour de France Stage 8: Dole - Station des Rousses'
        },

        subtitle: {
            text: 'An annotated chart in Highcharts'
        },

        annotations: [{
            labelOptions: {
                backgroundColor: 'rgba(255,255,255,0.5)',
                verticalAlign: 'top',
                y: 15
            },
            labels: [{
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 27.98,
                    y: 255
                },
                text: 'Arbois'
            }, {
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 45.5,
                    y: 611
                },
                text: 'Montrond'
            }, {
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 63,
                    y: 651
                },
                text: 'Mont-sur-Monnet'
            }, {
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 84,
                    y: 789
                },
                x: -10,
                text: 'Bonlieu'
            }, {
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 129.5,
                    y: 382
                },
                text: 'Chassal'
            }, {
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 159,
                    y: 443
                },
                text: 'Saint-Claude'
            }]
        }, {
            labels: [{
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 101.44,
                    y: 1026
                },
                x: -30,
                text: 'Col de la Joux'
            }, {
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 138.5,
                    y: 748
                },
                text: 'Côte de Viry'
            }, {
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 176.4,
                    y: 1202
                },
                text: 'Montée de la Combe<br>de Laisia Les Molunes'
            }]
        }, {
            labelOptions: {
                shape: 'connector',
                align: 'right',
                justify: false,
                crop: true,
                style: {
                    fontSize: '0.8em',
                    textOutline: '1px white'
                }
            },
            labels: [{
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 96.2,
                    y: 783
                },
                text: '6.1 km climb<br>4.6% on avg.'
            }, {
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 134.5,
                    y: 540
                },
                text: '7.6 km climb<br>5.2% on avg.'
            }, {
                point: {
                    xAxis: 0,
                    yAxis: 0,
                    x: 172.2,
                    y: 925
                },
                text: '11.7 km climb<br>6.4% on avg.'
            }]
        }],

        xAxis: {
            labels: {
                format: '{value} km'
            },
            minRange: 5,
            title: {
                text: 'Distance'
            }
        },

        yAxis: {
            startOnTick: true,
            endOnTick: false,
            maxPadding: 0.35,
            title: {
                text: null
            },
            labels: {
                format: '{value} m'
            }
        },

        tooltip: {
            headerFormat: 'Distance: {point.x:.1f} km<br>',
            pointFormat: '{point.y} m a. s. l.',
            shared: true
        },

        legend: {
            enabled: false
        },

        series: [{
            data: elevationData,
            lineColor: Highcharts.getOptions().colors[1],
            color: Highcharts.getOptions().colors[2],
            fillOpacity: 0.5,
            name: 'Elevation',
            marker: {
                enabled: false
            },
            threshold: null
        }]

    }
    }
  }
}
</script>

<style>
</style>
