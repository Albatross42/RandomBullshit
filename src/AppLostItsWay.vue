<template>
  <b-container fluid class="bv-example-row">
    <b-row>
      <div>
        <h3>Import XLSX</h3>
        <xlsx-read :file="file">
          <input type="file" @change="onChange" />
        </xlsx-read>
      </div>
    </b-row>
    <b-row>
      <!-- Guidlines -->
      <b-col style="border:1px solid #0000FF;">
      1 of 7
      </b-col>
      <!-- Safety -->
      <b-col style="border:1px solid #0000FF;padding: 0px;">
        <vc-calendar :attributes='safetyCal' is-expanded sm></vc-calendar>
      </b-col>
      <!-- Quality -->
      <b-col style="border:1px solid #0000FF;padding: 0px;"></b-col>
    </b-row>
  </b-container>
</template>

<script>
import Vue from 'vue';
import VCalendar from 'v-calendar';
import { XlsxRead } from '/node_modules/vue-xlsx/dist/vue-xlsx.es.js';
import * as XLSX from "xlsx/xlsx.mjs";


// Use v-calendar & v-date-picker components
Vue.use(VCalendar, {
  componentPrefix: 'vc'  // Use <vc-calendar /> instead of <v-calendar />
});

export default {
  name: 'App',
  components: {
    XlsxRead,
  },
  data() {
    return {
      file: null,
      safetyCal: [
        {
          highlight: 'red',
          dates: new Date(2022, 9, 1),
        }
      ],
    };
  },
  methods: {
    onChange(event) {
      this.file = event.target.files ? event.target.files[0] : null;
      var apple = this.file;
      const reader = new FileReader();

        /* Convert XLSX to JSON */
        reader.onload = (e) => {
          const bstr = e.target.result;
          const wb = XLSX.read(bstr, { type: 'binary' });
          const wsname = wb.SheetNames[0];
          const ws = wb.Sheets[wsname];
          const data = XLSX.utils.sheet_to_json(ws, { header: 1 });

          /*console.log(data);
          console.log(this.safetyCal[0].highlight);
          console.log(data[1][1]);*/

          /* Populate the Calendar */
          data.forEach((value, index ) => {
            if (value[1] == 'yes') {
              let NewCal = {
                highlight: 'green',
                dates: new Date(2022, 9, index),
                }
              this.safetyCal.push(NewCal);  
            } else if (value[1] == 'no') {
              let NewCal = {
                highlight: 'red',
                dates: new Date(2022, 9, index),
                }
              this.safetyCal.push(NewCal); 
            }
          });
        }
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