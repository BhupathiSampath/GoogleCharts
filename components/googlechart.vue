<template>
  <div>
    <h2>Google Bar Chart Demo</h2>
    <GChart
      type="ColumnChart"
      :key="random"
      :options="options"
      :data="data"
    />    
  </div>
</template>
 
<script>
import { GChart } from "vue-google-charts";
import axios from 'axios'
export default {
  name: "App",
  components: {
    GChart
  },
  data() {
    return {
      random: Math.random(),
      chartdata: [],
      data: [],
      options: {
        width: 1100,
        height: 400
      }
    };
  },
    async created() {
    const data1 = await axios.get(`http://127.0.0.1:8000/api/googlchart/`)
    this.data = data1.data
    this.random =Math.random()

    
  },
};
</script>