<template>
  <div class="chartElem">
    <section class="column">
      <highcharts class="chart" :options="chartOptions" :updateArgs="updateArgs"></highcharts>
    </section>
    <section class="column">
      <div class="row">
        <div>
          <h3>Change the labels:</h3>
          <h4>Categories:</h4>
          <div v-for="(label, index) in chartOptions.xAxis.categories" :key="index">
            <input v-model="chartOptions.xAxis.categories[index]"/>
          </div>
          <!-- <label>Max Lines
            <input type="number" v-model="maxLines">
          </label> -->
        </div>
      </div>
      <div class="row">
        <div id="title">
          <h3>Set chart title dynamically:</h3>
          <input type="text" v-model="title"/>
        </div>
        <div id="chartType">
          <h3>Select chart type:</h3>
          <select v-model="chartType">
            <option>Spline</option>
            <option>AreaSpline</option>
            <option>Line</option>
            <option>Scatter</option>
            <option>Column</option>
            <option>Area</option>
          </select>
        </div>
        <div id="animationDuration">
          <h3>Select update animation duration:</h3>
          <select v-model="animationDuration" type="number">
            <option>0</option>
            <option>500</option>
            <option>1000</option>
            <option>2000</option>
          </select>
        </div>
        <div id="seriesColor">
          <h3>Select color of the series:</h3>
          <div class="row" v-for="(participant, index) in chartOptions.series" :key="index">
            <p style="display: inline-block; margin-right: 1rem;">{{participant.name}}</p>
            <input
              id="colorPicker"
              v-if="colorInputIsSupported"
              type="color"
              :value="seriesColor(index)"
              @change="updateColor($event, index)"
            />
            <select v-else v-model="seriesColor">
              <option>Red</option>
              <option>Green</option>
              <option>Blue</option>
              <option>Pink</option>
              <option>Orange</option>
              <option>Brown</option>
              <option>Black</option>
              <option>Purple</option>
            </select>
          </div>
        </div>
      </div>
      </section>
  </div>
</template>

<script>
import { Chart } from "highcharts-vue";
export default {
  components: {
    highcharts: Chart
  },
  data() {
    return {
      title: "Stacked bar chart",
      points: [10, 0, 8, 2, 6, 4, 5, 5],
      maxLines: 5,
      titleUpdated: false,
      chartType: "Bar",
      colorInputIsSupported: null,
      animationDuration: 1000,
      updateArgs: [true, true, { duration: 1000 }],
      chartOptions: {
        chart: {
          type: "bar"
        },
        title: {
          text: "Stacked bar chart"
        },
        xAxis: {
          categories: [
            "More at each you 44 epic cooperative the game. 44 carry increase number future Unlike is. For 2 production wil cards the wil.",
            "City the over in low to high you to on the. You games  an game to game no you 2, Unlike Panic triggered to game  an cooperative. Triggered of actions another ability actions epic at number future cards, games infection location for. Whats against is number cards players game triggered number. Unused all the number wil units Whats in, epic the one another ability.",
            "End you you number for, some deck epic is this resolve location some. Another ability units of end on the is the. Some against in Unlike deck games future to.",
            "City the over in low to high you to on the. You games  an game to game no you 2, Unlike Panic triggered to game  an cooperative. Triggered of actions another ability actions epic at number future cards, games infection location for. Whats against is number cards players game triggered number. Unused all the number wil units Whats in, epic the one another ability.",
            "Production cooperative Panic most epic, take wil end for cooperative. The future games units this to game epic in. Low to high another ability unused units, Whats based cooperative Panic in 44  an infection games.  an increase games, of for location number Whats working players. Games Whats game to game over, one unused in number working Whats Total you the. Carry of game location take wil game end. Triggered spend at low to high the, unused 44 to low to high infection the. You most wil you, to is carry based resolve game triggered the you games. Of upgrades number upgrades no of production future Total."
          ],
          labels: {
            style: {
              textOverflow: "none"
            },
            formatter: function() {
              return `<div class="label">${this.value}</div>`;
            },
            useHTML: true
          }
        },
        yAxis: {
          min: 0,
          title: {
            text: "Total fruit consumption"
          }
        },
        legend: {
          reversed: true
        },
        plotOptions: {
          series: {
            stacking: "normal"
          }
        },
        tooltip: {
          useHTML: true,
          shadow: false,
          formatter: function() {
            return (
              `<div class="tooltip"><b>` +
              this.series.name +
              "</b>" +
              '<br><div class="tooltip-text">' +
              this.x +
              "</div" +
              "</div>"
            );
          }
        },
        series: [
          {
            name: "John",
            color: '#eeeeee',
            data: [5, 3, 4, 7, 2]
          },
          {
            name: "Jane",
            color: '#eeeeee',
            data: [2, 2, 3, 2, 1]
          },
          {
            name: "Joe",
            color: '#eeeeee',
            data: [3, 4, 4, 2, 5]
          }
        ]
      }
    };
  },
  created() {
    let i = document.createElement("input");
    i.setAttribute("type", "color");
    i.type === "color"
      ? (this.colorInputIsSupported = true)
      : (this.colorInputIsSupported = false);
  },
  watch: {
    title(newValue) {
      this.titleUpdated = true
      this.chartOptions.title.text = newValue;
    },
    points(newValue, idx) {
      this.chartOptions.series[idx].data = newValue;
    },
    chartType(newValue) {
      this.chartOptions.chart.type = newValue.toLowerCase();
      if (!this.titleUpdated) {
        this.chartOptions.title.text = newValue
      }
    },
    seriesColor(newValue) {
      this.chartOptions.series[0].color = newValue.toLowerCase();
    },
    animationDuration(newValue) {
      this.updateArgs[2].duration = Number(newValue);
    }
  },
  methods: {
    seriesColor(idx) {
      return this.chartOptions.series[idx].color
    },
    updateColor($event, idx) {
      this.chartOptions.series[idx].color = $event.target.value
    }
  }
};
</script>

<style scoped>
.chartElem {
  display: flex;
  flex-flow: row-reverse nowrap;
  justify-content: space-around;
}
.chart {
  min-height: 50rem;
}
input[type="color"]::-webkit-color-swatch-wrapper {
  padding: 0;
}
#colorPicker {
  border: 0;
  padding: 0;
  margin: 0;
  width: 30px;
  height: 30px;
}
.numberInput {
  width: 30px;
}

input,
select {
  width: 100%;
  max-width: 20rem;
  background: #eee;
  border: 0;
}

.data-inputs {
  display: flex;
  flex-flow: row nowrap;
}

.numberInput {
  width: 100%;
  margin: 0.5rem 2rem;
}

::v-deep .tooltip {
  background: white;
  padding: .25rem .5rem;
  opacity: 1;
}
::v-deep .tooltip-text {
  white-space: normal;
  width: 40rem;
  max-width: 100%;
}
::v-deep .label {
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 5;
  -webkit-box-orient: vertical;
}
</style>