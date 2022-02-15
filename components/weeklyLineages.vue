<template>
  <v-chart class="chart" :option="option"></v-chart>
</template>

<script>
import { map } from 'lodash'
import axios from 'axios'
import * as echarts from 'echarts/core'
import {
  TooltipComponent,
  GridComponent,
  LegendComponent,
  MarkLineComponent,
} from 'echarts/components'
import { BarChart } from 'echarts/charts'
import { CanvasRenderer } from 'echarts/renderers'
echarts.use([
  TooltipComponent,
  GridComponent,
  LegendComponent,
  MarkLineComponent,
  BarChart,
  CanvasRenderer,
])
import VChart from 'vue-echarts'

export default {
  name: 'HelloWorld',
  components: {
    VChart,
  },
  provide: {
    // [THEME_KEY]: 'dark',
  },
  data() {
    return {
      option: {
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow',
          },
        },
        legend: {
            data: []
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
        //   containLabel: true,
        },
        xAxis: [
          {
            type: 'category',
            data: [],
          },
        ],
        yAxis: [
          {
            type: 'value',
          },
        ],
        series: [],
      },
    }
  },
	async created() {
    const data = await axios.get(`http://127.0.0.1:8000/api/weeklystackbar/`);
    this.option.xAxis[0].data = data.data.week.week_number
      let s = map(data.data.lineage, (d) => ({
        name: d.lineage,
        type: 'bar',
        stack: 'Ad',
        emphasis: {
            focus: 'series'
        },
        data: d.value,
      }))
      this.option.series = s
    }
}
</script>

<style scoped>
.chart {
  height: 500px;
}
</style>
