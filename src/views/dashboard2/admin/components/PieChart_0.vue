<template>
  <div>
    <mallki class-name="mallki-text" text="肌肉組成" />
    <br>
    <div ref="chart" :class="className" :style="{height:height,width:width}" />
  </div>
</template>

<script>
import echarts from 'echarts'

require('echarts/theme/macarons') // echarts theme
import resize from './mixins/resize'
import Mallki from '@/components/TextHoverEffect/Mallki.vue'

export default {
  components: { Mallki },
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
      default: '420px'
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
      this.chart = echarts.init(this.$refs.chart, 'macarons')

      this.chart.setOption({
        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b} : {c} ({d}%)'
        },
        legend: {
          left: 'center',
          bottom: '10',
          data: ['肌肉生理張力', '肌肉硬度', '最大瞬時力矩']
        },
        series: [
          {
            name: '肌肉質量狀態：',
            type: 'pie',
            roseType: 'radius',
            radius: ['7%', '50%'],
            center: ['50%', '42%'],
            data: [
              { value: 320, name: '肌肉生理張力' },
              { value: 240, name: '肌肉硬度' },
              { value: 149, name: '最大瞬時力矩' }
            ],
            animationEasing: 'cubicInOut',
            animationDuration: 2600
          }
        ]
      })
    }
  }
}
</script>
