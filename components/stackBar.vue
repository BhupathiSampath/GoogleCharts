<template>
  <v-chart class="chart" :option="option"/>
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
import VChart, { THEME_KEY } from 'vue-echarts'

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
        legend: {},
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
        //   containLabel: true,
        },
        xAxis: [
          {
            type: 'category',
            data: ["2020-Jan","2020-Feb","2020-Mar","2020-Apr","2020-May","2020-Jun","2020-Jul","2020-Aug","2020-Sep","2020-Oct","2020-Nov","2020-Dec","2021-Jan","2021-Feb","2021-Mar","2021-Apr","2021-May","2021-Jun","2021-Jul","2021-Aug","2021-Sep","2021-Oct","2021-Nov","2021-Dec","2022-Jan","2022-Feb"],
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
    const data = await axios.get(`http://127.0.0.1:8000/api/monthlylinclassification/`);
    this.option.xAxis.data = data.data.month.month_number
    // console.log(data.data.lineage)
    let only_name = map(data.data.lineage, (d) => d.name)
      let s = map(data.data.lineage, (d) => ({
        // stack: true,
        name: d.Class,
        type: 'bar',
        stack: 'Ad',
        emphasis: {
            focus: 'series'
        },
        // smooth: true,
        // silent: true,
        data: d.value,
        // showSymbol: false,
        // label: { show: false },
        // lineStyle: { width: 0 },
        // areaStyle: { opacity: 1 },
      }))
      this.option.series = s
    //   this.option.legend.data = only_name
    // console.log(this.option.xAxis.data)
    console.log(this.option.series)
    }
}
</script>

<style scoped>
.chart {
  height: 500px;
}
</style>
