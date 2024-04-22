<template>
  <div>
    <mallki class-name="mallki-text" text="肌肉組成" />
    <br>
    <!--    <div ref="chart" :class="className" :style="{ height: height, width: width }"/>-->
    <ul>
      <li v-for="person in persons" :key="person.person_id">
        <p>{{ person.person_id }}</p>
        <p>Name: {{ person.name }}</p>
        <p>Gender: {{ person.gender }}</p>
        <p>Age: {{ person.age }}</p>
      </li>
    </ul>
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
      chart: null,
      persons: [] // 使用数组存储所有个人信息
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.initChart()
      this.fetchData()
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
        // 省略图表配置
      })
    },
    fetchData() {
      fetch('http://163.18.44.158:9000/person_view/?format=json')
        .then(response => response.json())
        .then(data => {
          this.persons = data.results
        })
    }
  }
}
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

a {
  text-decoration: none;
}

ul {
  margin: 0;
  padding: 0;
}

li {
  list-style: none;
}

.card {
  margin-bottom: 50px;
  text-align: center;
}

.card-img {
  width: 128px;
  height: 128px;
  margin: 0 auto 10px auto;
  overflow: hidden;
  border-radius: 50%;
  img {
    border-radius: 50%;
  }
}

.prev-img-enter-active,
.prev-img-leave-active,
.next-img-enter-active,
.next-img-leave-active {
  transition: all 0.5s;
}

.next-img-leave-to {
  transform: translate(-100%);
}

.prev-img-leave-to {
  transform: translate(100%);
}

.carousel-btns {
  a {
    color: #7b7b7b;
  }

  display: flex;
  justify-content: center;
  align-items: center;
}

.carousel-btn {
  border-radius: 50%;
  background: #ededed;
  width: 10px;
  height: 10px;
  margin: 0 10px;

  &-active {
    background: royalblue;
  }

  &-group {
    margin: 0 10px;
    display: flex;
    justify-content: center;
  }
}
</style>
