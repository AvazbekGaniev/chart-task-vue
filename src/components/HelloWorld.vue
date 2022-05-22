<template>
  <div className="app">
    <Bar
        :chart-options="options"
        :chart-data="chartData"
        :chart-id="chartId"
        :dataset-id-key="datasetIdKey"
        :plugins="plugins"
        :css-classes="cssClasses"
        :styles="styles"
        :width=1200
        :height=400

    />
  </div>

</template>

<script>
import {Bar} from 'vue-chartjs'
import {Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale} from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)


export default {
  name: 'HelloWorld',
  components: {Bar},
  props: {
    chartId: {
      type: String,
      default: 'bar'
    },
    datasetIdKey: {
      type: String,
      default: 'label'
    },
    cssClasses: {
      default: '',
      type: String
    },
    styles: {
      type: Object,
      default: () => {
        return {
          borderDash: [20, 5]
        }
      }
    },
    plugins: {
      type: Object,
      default: () => {
        return {
          legend: {
            position: 'top',
          },
          title: {
            display: true,
            text: 'Chart.js Horizontal Bar Chart'
          }
        }
      }
    }
  },
  data() {
    return {
      chartData: {
        labels: [
          0,
          1,
          2,
          3,
          4,
          5,
          6
        ], // Date Objects
        datasets: [
          {
            label: "min",
            backgroundColor: "rgba(240, 140, 121, 1.0)",
            borderColor: "rgba(140, 140, 140, 0.0)",
            borderWidth: 0,
            data: [
              [5,10],
              [7,20],
              [10,15],
              [20,25],
              [30,40],
              [27,35],
              [10,32],
            ],
            fill: "-1",
            radius: 0,
          },
          {
            label: "test",
            backgroundColor: "rgb(80,55,51)",
            borderColor: "rgba(173,24,24,0)",
            borderWidth: 0,

            data: [
              [10, 12],
              [20, 25],
              [15, 25],
              [25, 28],
              [40, 41],
              [35, 42],
              [32, 34],
            ],
            fill: "-1",
            radius: 0,
          },
          {
            label: "max",
            backgroundColor: "rgba(121, 200, 121, 0.8)",
            borderColor: "rgba(140, 140, 140, 0.0)",
            borderWidth: 0,
            data: [
              [12, 18],
              [25, 28],
              [25, 35],
              [28, 29],
              [41, 51],
              [42, 55],
              [34, 43]
            ],
            fill: "-1",
            line: false,
            radius: 0,
          },
        ]
      },
      options: {
        tooltips: {
          mode: 'index',
          intersect: false,
          displayColors: false,
        },
        responsive: false,
        title: {
          display: true,
          text: "Chart.js stackable with Min/Avg/Max"
        },
        indexAxis: 'y',
        scales: {
          y: {
            drawBorder: false,
            grid : {
            color: null,
            },
            stacked: true,
            time: {
              // Luxon format string
              tooltipFormat: 'DD T'
            },
            format: "HH mm",
          },
          x: {
            stacked: false,
            scaleLabel: {
              display: true,
              labelString: "value"
            }
          },
          x1: {
            type: 'linear',
            display: true,
            position: 'top',

            // grid line settings
            grid: {
              drawOnChartArea: false, // only want the grid lines for one axis to show up
            }
          },
        },
        pan: {
          enabled: true,
          mode: "x",
          speed: 10,
          threshold: 10
        },
        zoom: {
          enabled: true,
          drag: false,
          mode: "xy",
          limits: {
            max: 10,
            min: 0.5
          }
        }
      }
    }
  }
}

</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bar {
  width: 9000px;
  height: 300px;
}
</style>
