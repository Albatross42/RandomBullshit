<template>
  <LineChartGenerator :chart-options="chartOptions" :chart-data="chartData" :chart-id="chartId"
    :dataset-id-key="datasetIdKey" :plugins="plugins" :css-classes="cssClasses" :styles="styles" :width="width"
    :height="height" />
</template>

<script>
import { Line as LineChartGenerator } from 'vue-chartjs/legacy'

import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  CategoryScale,
  PointElement
} from 'chart.js'

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  CategoryScale,
  PointElement
)

export default {
  name: 'LineChart',
  components: {
    LineChartGenerator
  },
  props: {
    chartId: {
      type: String,
      default: 'line-chart'
    },
    datasetIdKey: {
      type: String,
      default: 'label'
    },
    width: {
      type: Number,
      default: 200
    },
    height: {
      type: Number,
      default: 200
    },
    cssClasses: {
      default: '',
      type: String
    },
    styles: {
      type: Object,
      default: () => { }
    },
    plugins: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      chartData: {
        //  labels: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31],
        // labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
        datasets: [
          {
            label: 'Daily Trend Chart',
            // data: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31],

            data: [
              { x: '1', y: 1 },
              { x: '2', y: 2 },
              { x: '3', y: 3 },
              { x: '4', y: 4 },
              { x: '5', y: 5 },
              { x: '6', y: 6 },
              { x: '7', y: 7 },
              { x: '8', y: 8 },
              { x: '9', y: 9 },
              { x: '10', y: 10 },
              { x: '11', y: 11 },
              { x: '12', y: 12 },
              { x: '13', y: 13 },
              { x: '14', y: 14 },
              { x: '15', y: 15 },
              { x: '16', y: 16 },
              { x: '17', y: 17 },
              { x: '18', y: 18 },
              { x: '19', y: 19 },
              { x: '20', y: 20 },
              { x: '21', y: 21 },
              { x: '22', y: 22 },
              { x: '23', y: 23 },
              { x: '24', y: 24 },
              { x: '25', y: 25 },
              { x: '26', y: 26 },
              { x: '27', y: 27 },
              { x: '28', y: 28 },
              { x: '29', y: 29 },
              { x: '30', y: 30 },
              { x: '31', y: 31 },
            ],

            fill: false,
            borderColor: 'blue',
            backgroundColor: 'blue',
            tension: 0.1
          }
        ]
      },
      chartOptions: {
        responsive: false,
        maintainAspectRatio: true,
        normalized: true // Chart.js is fastest if you provide data with indices that are unique sorted and consistent across datasets and provide the normalized: true option to let Chart.js know that you have done so.
      }
    }
  }
}
</script>
