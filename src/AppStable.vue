<template>
  <b-container fluid class="bv-example-row">
    <b-row>Title</b-row>
    <b-row>
      <!-- Guidlines -->
      <b-col style="border:1px solid #0000FF;">
      1 of 7
      </b-col>
      <!-- Safety -->
      <b-col style="border:1px solid #0000FF;padding: 0px;"><vc-calendar :attributes='safetyCal' is-expanded sm></vc-calendar></b-col>
      <!-- Quality -->
      <b-col style="border:1px solid #0000FF;padding: 0px;"><vc-calendar></vc-calendar></b-col>
      <!-- Delivery -->
      <b-col style="border:1px solid #0000FF;padding: 0px;"></b-col>
      <!-- Inventory -->
      <b-col style="border:1px solid #0000FF;padding: 0px;"></b-col>
      <!-- Productivity -->
      <b-col style="border:1px solid #0000FF;padding: 0px;"></b-col>
      <!-- Extra Info -->
      <b-col style="border:1px solid #0000FF;padding: 0px;"> 7 of 7</b-col>
    </b-row>
  </b-container>
</template>

<script>
import Vue from 'vue';
import VCalendar from 'v-calendar';

// Use v-calendar & v-date-picker components
Vue.use(VCalendar, {
  componentPrefix: 'vc'  // Use <vc-calendar /> instead of <v-calendar />
});

export default {
  name: 'App',
  components: {},
    data() {

    return {
      safetyCal: [
        {
          highlight: 'red',
          dates: new Date(2022, 9, 1),
        }
      ],
    };
  },
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
