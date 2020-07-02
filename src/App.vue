<template>
  <v-app>
    
    <v-content>
      <Navbar/>
      <test/>
     <HelloWorld/>
     <v-card class="mx-auto" max-width="500">
      <!-- <LineChart/> -->
     </v-card>
      
      
    </v-content>
    
  </v-app>
</template>

<script>
//import LineChart from './components/LineChart'
//import Dashboard from './views/Dashboard'
import Navbar from './components/Navbar'
import test from './components/test'
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',

  components: {
    Navbar,
    test,
    //LineChart,
    //Dashboard,
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
