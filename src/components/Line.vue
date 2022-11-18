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
        labels: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31],
        // labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
        datasets: [
          {
            label: 'Daily Trend Chart',
            data: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31],
            /* 
            data: [
              { x: 'Jan', y: 20 },
              { x: 'Feb', y: 10 },
              { x: 'Mar', y: 69 },
              { x: 'Apr', y: 4 },
              { x: 'May', y: 20 },
              { x: 'Jun', y: 35 },
              { x: 'Jul', y: 45 },
              { x: 'Aug', y: 25 },
              { x: 'Sep', y: 33 },
              { x: 'Oct', y: 56 },
              { x: 'Nov', y: 10 },
              { x: 'Dec', y: 0 },
            ], 
            */
            borderColor: 'blue',
            backgroundColor: 'blue'
          }
        ]
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
        normalized: true // Chart.js is fastest if you provide data with indices that are unique sorted and consistent across datasets and provide the normalized: true option to let Chart.js know that you have done so.
      }
    }
  }
}
</script>
