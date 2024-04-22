<template>
  <div ref="chartRef" :class="className" :style="{height:height,width:width}" />
</template>

<script>
import echarts from 'echarts'

require('echarts/theme/macarons') // echarts theme
import resize from './mixins/resize'

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
    },
    data: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      chart: null
    }
  },
  watch: {
    data: {
      handler: 'updateChart',
      immediate: true
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
      this.chart = echarts.init(this.$refs.chartRef, 'macarons')
      this.updateChart()
    },
    updateChart() {
      if (!this.chart || !this.data || this.data.length === 0) {
        return
      }
      const selectedLabels = ['severity_A', 'severity_B', 'severity_C', 'severity_D']
      const xAxisData = selectedLabels
      const seriesData = this.data.map(item => selectedLabels.map(label => item[label]))
      this.chart.setOption({
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
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
          data: xAxisData,
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
        series: seriesData.map((data, index) => ({
          name: `Series ${index + 1}`,
          type: 'bar',
          data,
          animationDuration: 6000
        }))
      })
    }
  }
}
</script>
