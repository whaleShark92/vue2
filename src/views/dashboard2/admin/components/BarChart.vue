<template>
  <div :class="className" :style="{height:height,width:width}" />
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
import resize from './mixins/resize'

const animationDuration = 6000

export default {
  mixins: [resize],
  props: {
    className: {
      type: String,
      default: 'chart'
    },
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '300px'
    }
  },
  data() {
    return {
      chart: null
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.initChart()
    })
  },
  beforeDestroy() {
    if (!this.chart) {
      return
    }
    this.chart.dispose()
    this.chart = null
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$el, 'macarons')

      this.chart.setOption({
        tooltip: {
          trigger: 'axis',
          axisPointer: { // 坐标轴指示器，坐标轴触发有效
            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
          }
        },
        grid: {
          top: 10,
          left: '2%',
          right: '2%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: [{
          type: 'category',
          data: ['Frequency', 'Stiffness', 'Peak T', 'Average Peak T'],
          axisTick: {
            alignWithLabel: true
          }
        }],
        yAxis: [{
          type: 'value',
          axisTick: {
            show: false
          }
        }],
        // series: [{
        //   name: 'Net Profit',
        //   data: [44, 55, 57, 56, 61, 58, 63, 60, 66]
        // }, {
        //   name: 'Revenue',
        //   data: [76, 85, 101, 98, 87, 105, 91, 114, 94]
        // }, {
        //   name: 'Free Cash Flow',
        //   data: [35, 41, 36, 26, 45, 48, 52, 53, 41]
        // }]
        series: [{
          name: 'before',
          type: 'bar',
          // stack: 'vistors',
          // barWidth: '60%',
          data: [17.52, 354.19, 90.71, 82.39],
          animationDuration
        }, {
          name: 'after',
          type: 'bar',
          // stack: 'vistors',
          // barWidth: '60%',
          data: [17.89, 366.92, 92.54, 82.39],
          animationDuration
        }]
      })
    }
  }
}
</script>
