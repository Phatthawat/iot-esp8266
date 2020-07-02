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
      <v-card>
      <apexchart type="area" height="350" :options="chartOptions" :series="series"></apexchart>
      </v-card>
      </div>


      
    </v-content>
     

<!-- Sparkline
    <v-container fluid>
    <v-sparkline
      :value="value"
      :gradient="gradient"
      :smooth="radius || false"
      :padding="padding"
      :line-width="lineWidth"
      :stroke-linecap="lineCap"
      :gradient-direction="gradientDirection"
      :fill="fill"
      :type="type"
      :auto-line-width="autoLineWidth"
      auto-draw
      :show-labels="showLabels"
      :label-size="labelSize"
    ></v-sparkline>

    <v-divider></v-divider>

    <v-row>
      <v-col v-if="showLabels" cols="12">
        <v-slider
          v-model="labelSize"
          label="Label size"
          min="1"
          max="20"
          thumb-label
        ></v-slider>
      </v-col>
    </v-row>
  </v-container> -->



  </v-card>
    </v-container>
</template>

<script>
import VueApexCharts from 'vue-apexcharts'

/*const gradients = [
    ['#222'],
    ['#42b3f4'],
    ['red', 'orange', 'yellow'],
    ['purple', 'violet'],
    ['#00c6ff', '#F0F', '#FF0'],
    ['#f72047', '#ffd200', '#1feaea'],
  ]

  var dataTemp = [2,5,6,7,0,50,60,70,0,90];*/
var dataTemp = [2,5,8,10,11,30,100];
var dataHumid = [2,5,8,10,11,30,100];


export default {
  component:{
    VueApexCharts
  },



  data() {
    return {

      wsUrl:'ws://127.0.0.1:1880/websocket',
      socket: null,
      counter:0,
      connState: false,
      msg:'',
      temperature:0,
      humidity:0,

  series: [{
            name: "Temperature",
            data: dataTemp,
          }, {
            name: "Humidity",
            data: dataHumid
          }],
      /*****************************

      showLabels: false,
      lineWidth: 2,
      labelSize: 7,
      radius: 10,
      padding: 8,
      lineCap: 'round',
      gradient: gradients[5],
      value: dataTemp,
      gradientDirection: 'top',
      gradients,
      fill: true,
      type: 'trend',
      autoLineWidth: false,

*/
          chartOptions: {
            chart: {
              height: 100,
              type: 'radialBar',
              toolbar: {
                show: false
              }
            },
            plotOptions: {
              radialBar: {
                startAngle: -135,
                endAngle: 225,
                 hollow: {
                  margin: 0,
                  size: '67%',
                  background: '#fff',
                  image: undefined,
                  imageOffsetX: 0,
                  imageOffsetY: 0,
                  position: 'front',
                  dropShadow: {
                    enabled: true,
                    top: 3,
                    left: 0,
                    blur: 4,
                    opacity: 0.24
                  }
                },
                track: {
                  background: '#fff',
                  strokeWidth: '50%',
                  margin: 0, // margin is in pixels
                  dropShadow: {
                    enabled: true,
                    top: -3,
                    left: 0,
                    blur: 4,
                    opacity: 0.35
                  }
                },
            
                dataLabels: {
                  show: true,
                  name: {
                    offsetY: -10,
                    show: true,
                    color: '#888',
                    fontSize: '17px'
                  },
                  value: {
                    formatter: function(val) {
                      return parseInt(val);
                    },
                    color: '#111',
                    fontSize: '36px',
                    show: true,
                  }
                }
              }
            },
            fill: {
              type: 'gradient',
              gradient: {
                shade: 'dark',
                type: 'horizontal',
                shadeIntensity: 0.5,
                gradientToColors: ['#ABE5A1'],
                inverseColors: true,
                opacityFrom: 1,
                opacityTo: 1,
                stops: [0, 100]
              }
            },
            stroke: {
              lineCap: 'round'
            },
            labels: ['Percent'],
          },
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

      dataTemp.push(dataObject.temperature);
      chart.updateSeries([dataObject.temperature])
      chart.updateSeries([
        {
          name:"Temperature",
          data: dataTemp
        },
      ])
    }
  },
}
</script>

<style>
  
</style>
