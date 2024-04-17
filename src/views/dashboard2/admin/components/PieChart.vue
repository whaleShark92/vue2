<template>
  <div>
    <mallki class-name="mallki-text" text="控制台" />
    <br><br> <!-- 這裡插入兩個 <br> 標籤來增加行與行之間的距離 -->
    <!--    <div ref="chart" :class="className" :style="{height:height,width:width}"/>-->
    <!--    <el-col :span="6">-->
    <!--      <el-card class="box-card">-->
    <!--        <div slot="header" class="clearfix">-->
    <!--          <span>水波纹 waves v-directive</span>-->
    <!--        </div>-->
    <!--        <div class="component-item">-->
    <el-button v-waves type="primary">
      Test
    </el-button>
    <el-button v-waves type="primary">
      Start
    </el-button>
    <el-button v-waves type="primary">
      Finish
    </el-button>
    <br> <!-- 插入 <br> 標籤增加行與行之間的距離 -->
    <div />
    <br> <!-- 插入 <br> 標籤增加行與行之間的距離 -->
    <!-- eslint-disable-next-line no-unused-vars -->
    <!--    <div>Now is: {{ picked }}</div>-->
    <!--    <br> &lt;!&ndash; 插入 <br> 標籤增加行與行之間的距離 &ndash;&gt;-->
    <!--        </div>-->
    <!--      </el-card>-->
    <!--    </el-col>-->
    <!--    <div style="margin-bottom:50px;">-->
    <!--      <el-col :span="4" class="text-center">-->
    <!--        <router-link class="pan-btn blue-btn" to="/documentation/index">-->
    <!--          Test-->
    <!--        </router-link>-->
    <!--      </el-col>-->
    <!--      <el-col :span="4" class="text-center">-->
    <!--        <router-link class="pan-btn light-blue-btn" to="/icon/index">-->
    <!--          Start-->
    <!--        </router-link>-->
    <!--      </el-col>-->
    <!--      <el-col :span="4" class="text-center">-->
    <!--        <router-link class="pan-btn pink-btn" to="/excel/export-excel">-->
    <!--          Finish-->
    <!--        </router-link>-->
    <!--      </el-col>-->
    <!--    </div>-->
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
