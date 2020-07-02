<template>

<v-container>



  <v-card class="ma-5" width="900" height="400">
    msg : {{msg}} <br>
    State : {{connState}}
    <v-card>
      <p>Temperature : {{ temperature }}</p>
      <apexchart type="radialBar" height="200" :options="chartOptions" :series="temperature"></apexchart>

      <p>Humidity : {{ humidity }}</p>
      <apexchart type="radialBar" height="200" :options="chartOptions" :series="humidity"></apexchart>
    </v-card>

    <v-spacer></v-spacer>

    <v-content class="mx-auto">

      <div id="chart">
        <apexchart type="area" height="350" :options="chartOptions" :series="series"></apexchart>
      </div>
      <v-card>
      </v-card>
    </v-content>

  </v-card>
    </v-container>
</template>

<script>
import VueApexCharts from 'vue-apexcharts'
import Vue from 'vue'
Vue.use(VueApexCharts)
Vue.component('apexchart', VueApexCharts)

var newData = [1,10,5,6,100,50,80];

export default {
  component:{
    VueApexCharts
  },
 
 data: function () {
  return {

  name: 'Vue Chart',
  wsUrl:'ws://127.0.0.1:1880/websocket',
  socket: null,
  counter:0,
  connState: false,
  msg:'',
  temperature:0,
  humidity:0,

   chartOptions: {
    chart: {
      id: 'vuechart-example',
    },
    xaxis: {
      categories: [1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998],
    },
   },
   series: [{
    name: 'Vue Chart',
    data: newData
   }]
  }
 },

 methods: {
  updateChart() {
   const max = 100;
   const min = 0;
   const newData = this.series[0].data.map(() => {
     return Math.floor(Math.random() * (max - min + 1)) + min
   })
   // In the same way, update the series option
   this.series = [{
    data: newData
   }]
  }
 },

  created(){
    this.socket = new WebSocket(this.wsUrl);
    this.socket.onopen = () => {
      this.connState=true;
    }
    this.socket.onmessage = (m) => {
      console.log(m);
      this.msg = m.data;
      var dataObject = JSON.parse(m.data);
      this.temperature = [dataObject.temperature];
      this.humidity = [dataObject.humidity];
    }
  },
}
</script>

<style>
  
</style>
