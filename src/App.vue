<template>
  <b-container fluid class="row-1">
    <b-row>
      <b-col>
        <div>
          <xlsx-read :file="file">
            <input type="file" @change="onChange" />
          </xlsx-read>
        </div>
      </b-col>
    </b-row>

    <b-row>
      <!-- Guidlines -->
      <b-col style="border:0px solid #0000FF;">
        <div style="margin bottom:400px;">
          <h3 style="text-align:center;">Guidelines</h3>
          <h5>Metric/Status</h5>
          <p style="border:1px solid #000000;padding: 10px;"><span style="color:red">Red</span> = Incidents<br><span
              style="color:green">Green</span> = No incidents</p>
          <h5>Humidity</h5>
          <p style="border:1px solid #000000;padding: 10px;">Notify Supervisor if humidity increases over 70%</p>
        </div>
        <div style="margin top:400px;">
          <b-img src="https://static.wixstatic.com/media/a9b923_0bfa3bd9aab2446ab3a815e7633bb43d~mv2.png" fluid
            alt="Responsive image"></b-img>
        </div>
      </b-col>

      <!-- Safety use Linechart v-if="loaded" to handle line chart updates after new data -->
      <b-col style="border:0px solid #0000FF;padding: 10px;">
        <h3 style="background-color:#28A5F7; color:white;text-align:center;">SAFETY</h3>
        <vc-calendar :disabled-dates='{ weekdays: [1, 7] }' :attributes='safetyCal' is-expanded sm></vc-calendar>
        <LineChart :chart-data="chartData" ref="line" />
        <LineChart :chart-data="chartData" ref="line" />
        <LineChart :chart-data="chartData" ref="line" />
      </b-col>

      <!-- Quality -->
      <b-col style="border:0px solid #0000FF;padding: 10px;">
        <h3 style="background-color:#E60075; color:white;text-align:center;">QUALITY</h3>
        <vc-calendar :disabled-dates='{ weekdays: [1, 7] }' :attributes='safetyCal' is-expanded sm></vc-calendar>
        <LineChart :chart-data="chartData" ref="line" />
        <LineChart :chart-data="chartData" ref="line" />
        <LineChart :chart-data="chartData" ref="line" />
      </b-col>

      <!-- Delivery -->
      <b-col style="border:0px solid #0000FF;padding: 10px;">
        <h3 style="background-color:#F3A118; color:white;text-align:center;">DELIVERY</h3>
        <vc-calendar :disabled-dates='{ weekdays: [1, 7] }' :attributes='safetyCal' is-expanded sm></vc-calendar>
        <LineChart :chart-data="chartData" ref="line" />
        <LineChart :chart-data="chartData" ref="line" />
        <LineChart :chart-data="chartData" ref="line" />
      </b-col>

      <!-- Inventory -->
      <b-col style="border:0px solid #0000FF;padding: 10px;">
        <h3 style="background-color:#A118F3; color:white;text-align:center;">INVENTORY</h3>
        <vc-calendar :disabled-dates='{ weekdays: [1, 7] }' :attributes='safetyCal' is-expanded sm></vc-calendar>
        <LineChart :chart-data="chartData" ref="line" />
        <LineChart :chart-data="chartData" ref="line" />
        <LineChart :chart-data="chartData" ref="line" />
      </b-col>

      <!-- Productivity -->
      <b-col style="border:0px solid #0000FF;padding: 10px;">
        <h3 style="background-color:#56E8D5; color:white;text-align:center;">PRODUCTIVITY</h3>
        <vc-calendar :disabled-dates='{ weekdays: [1, 7] }' :attributes='safetyCal' is-expanded sm></vc-calendar>
        <LineChart :chart-data="chartData" ref="line" />
        <LineChart :chart-data="chartData" ref="line" />
        <LineChart :chart-data="chartData" ref="line" />
      </b-col>

      <!-- Required Attendance / Rules / Standard Work Chart / PTO / 5S Audits -->
      <b-col style="border:0px solid #0000FF;">
        <div style="background-color:green; color:white;text-align:left;padding: 10px;">
          <h5>REQUIRED ATTENDANCE:</h5>
          <b-list-group>
            <b-list-group-item>- <b>Loren Cochrun</b> (Engineer)</b-list-group-item>
            <b-list-group-item>- <b>Shaun Lublink</b> (Lead Supe)</b-list-group-item>
            <b-list-group-item>- <b>Jovy Ortiz</b> (New Supe)</b-list-group-item>
            <b-list-group-item>- <b>Sokthea Lee</b> (Ole Pro)</b-list-group-item>
            <b-list-group-item>- <b>Philip Coloso</b> (Ace Opperator)</b-list-group-item>
          </b-list-group>
        </div>
        <br>
        <div style="background-color:green; color:white;text-align:left;padding: 10px;">
          <h5>RULES:</h5>
          <b-list-group>
            <b-list-group-item>1. Meeting is no more than 15 min</b-list-group-item>
            <b-list-group-item>2. Meeting is held daily</b-list-group-item>
            <b-list-group-item>3. Do not problem solve at meeting</b-list-group-item>
            <b-list-group-item>4. Actions are assign to 1 person who is present</b-list-group-item>
            <b-list-group-item>5. Safe place (no blame)</b-list-group-item>
            <b-list-group-item>6. Focus on today's status</b-list-group-item>
          </b-list-group>
        </div>
        <br>
        <div style="background-color:green; color:white;text-align:left;padding: 10px;">
          <h5>Standard Work Chart</h5>
          <p style="border:0px solid #000000;padding: 0px;">Text</p>
        </div>
        <br>
        <div style="background-color:green; color:white;text-align:left;padding: 10px;">
          <h5>PTO Calendar:</h5>
          <p style="border:0px solid #000000;padding: 0px;">Text</p>
        </div>
        <br>
        <div style="background-color:green; color:white;text-align:left;padding: 10px;">
          <h5>5S Audits:</h5>
          <p style="border:0px solid #000000;padding: 0px;">Text</p>
        </div>
      </b-col>
    </b-row>
    <b-row>
      <div style="margin top:400px;">
        <b-img src="https://static.wixstatic.com/media/a9b923_f59f3228fc1541c5aef89b7e8070bd11~mv2.png" fluid
          alt="Responsive image"></b-img>
      </div>
    </b-row>
  </b-container>
</template>

<script>
import Vue from 'vue';
import VCalendar from 'v-calendar';
import { XlsxRead } from '/node_modules/vue-xlsx/dist/vue-xlsx.es.js';
import * as XLSX from "xlsx/xlsx.mjs";
import LineChart from './components/Line.vue'


// Use v-calendar & v-date-picker components
Vue.use(VCalendar, {
  componentPrefix: 'vc'  // Use <vc-calendar /> instead of <v-calendar />
});

export default {
  name: 'App',
  components: {
    XlsxRead,
    LineChart,
  },
  data() {
    return {
      file: null,
      safetyCal: [
        {
          highlight: 'blue',
          dates: new Date(), // With no arguments, the Date() constructor creates a Date object set to the current date and time.
          disabledDates: { weekdays: [1, 7] },
        }
      ],
      // loaded: false,
      chartData: [],
    };
  },
  methods: {
    onChange(event) {
      // this.loaded = true
      this.file = event.target.files ? event.target.files[0] : null;
      var apple = this.file;
      const reader = new FileReader();
      // const chartInstance = this.$refs.line.getCurrentChart
      // const chartInstance = this.$refs.line.$data.chartData.datasets[0].data[1]
      const chartDataObject = this.$refs.line.$data.chartData.datasets[0]

      /* Convert XLSX to JSON */
      reader.onload = (e) => {
        const bstr = e.target.result;
        const wb = XLSX.read(bstr, { type: 'binary' });
        const wsname = wb.SheetNames[0];
        const ws = wb.Sheets[wsname];
        const data = XLSX.utils.sheet_to_json(ws, { header: 1, blankrows: false });
        // const calDataObject = this.$refs.line.$data.chartData.datasets[0];
        const chartDataObject = this.$refs.line.$data.chartData.datasets[0];


        /* Populate the Calendar */
        // index =+ 1 to make the corresponding day reflect properly
        data.forEach((value, index = + 1) => {
          // for weekdays: [2, 3, 4, 5, 6];
          if (value[2] == 0) {
            let NewCal = {
              dates: new Date(2022, 10, index),
              highlight: 'green',
              popover: {
                label: value[2] + ' incidents',
              }
            }
            this.safetyCal.push(NewCal);
            // console.log(value, index);
          } else if (value[2] > 0) {
            let NewCal = {
              dates: new Date(2022, 10, index),
              highlight: 'red',
              popover: {
                label: value[2] + ' incidents',
              }
            }
            this.safetyCal.push(NewCal);
            // console.log(value, index);
          }
          if (index < 32) {
            // this.$refs.line.$data.chartData.datasets[0].data[index] = value[0];
            // calDataObject.data[index] = value[2];
            chartDataObject.data[index] = value[2];
          }
        });
        this.chartData.datasets = chartDataObject;
        // chart.update();
        // console.log(this.safetyCal);
        // console.log(this.safetyCal[0].highlight);
        // console.log(data[1][2]);
        // console.log(chart);
        // console.log(this.chartData.datasets);
      }
      this.chartData.datasets = chartDataObject;
      // chartInstance.updateChart();
      reader.readAsBinaryString(apple);
    },
  }
};

</script>

<style lang="scss">
@import "~@/assets/scss/vendors/bootstrap-vue/index";

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>