<template>

</template>

<script>
import VueApexCharts from 'vue-apexcharts'



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
