<template>
  <section class="charts">
    <h3>Bar Chart</h3>
    <vue-highcharts :key="random" :options="options" ref="barChart"></vue-highcharts>
  </section>
</template>
<script>
import VueHighcharts from 'vue2-highcharts'
import Highcharts from 'highcharts'
import axios from 'axios'

export default {
  components: {
    VueHighcharts,
  },
  data() {
    return {
        random: Math.random(),
      week_number: [],
      week_data: [],
      options: {
        chart: {
          type: 'bar',
        },
        title: {
          text: 'Distribution',
        },
        xAxis: {
          categories: [],
          title: {
            text: null,
          },
        },
        yAxis: {
          min: 0,
          title: {
            text: 'value',
            align: 'high',
          },
          labels: {
            overflow: 'justify',
          },
        },
        tooltip: {
          valueSuffix: ' millions',
        },
        plotOptions: {
          bar: {
            dataLabels: {
              enabled: true,
            },
          },
        },
        legend: {
          layout: 'vertical',
          align: 'right',
          verticalAlign: 'top',
          x: -40,
          y: 80,
          floating: true,
          borderWidth: 1,
          backgroundColor:
            (Highcharts.theme && Highcharts.theme.legendBackgroundColor) ||
            '#FFFFFF',
          shadow: true,
        },
        credits: {
          enabled: false,
        },
        series: [
          {
            data: [],
          },
        ],
      },
    }
  },
  async created() {
    const data = await axios.get(`http://127.0.0.1:8000/api/distribution/`)
    // console.log(data.data)
    data.data.forEach((d) => {
      const { week_number, strain__count } = d
      this.week_number.push(week_number)
      this.week_data.push(strain__count)
    })
    this.options.xAxis.categories = this.week_number
    this.options.series[0].data = this.week_data
    this.random = Math.random()
    console.log(this.options.xAxis.categories)
    console.log(this.options.series[0].data)
  },
}
</script>
