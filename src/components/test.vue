<template>
  <div class="example">
    <apexchart ref="demoChart" width="500" :options="chartOptions" :series="series"></apexchart>
  </div>
</template>

<script>
import VueApexCharts from 'vue-apexcharts'

export default {
component:{
    VueApexCharts
  },
functionName: function() {
    this.$refs.demoChart.updateOptions({ colors: "#008FFB" })
  },
};

</script>

<style>

</style>