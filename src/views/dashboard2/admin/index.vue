<template>
  <div class="dashboard-editor-container">
    <panel-group @handleSetLineChartData="handleSetLineChartData" />

    <el-row style="background:#fff;padding:16px 16px 0;margin-bottom:32px;">
      <line-chart :chart-data="lineChartData" />
    </el-row>
    <!--    <el-row style="background:#fff;padding:16px 16px 0;margin-bottom:32px;">-->
    <!--      <mix-chart :chart-data="MixChartData"/>-->
    <!--    </el-row>-->
    <el-row style="background:#fff;padding:16px 16px 0;margin-bottom:32px;">
      <complex-table />
    </el-row>
    <!--    <MixChart />-->
    <el-row :gutter="32">
      <el-col :xs="24" :sm="24" :lg="8">
        <div class="chart-wrapper">
          <box-card />
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :lg="8">
        <div class="chart-wrapper">
          <pie-chart />
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :lg="8">
        <div class="chart-wrapper">
          <transaction-table />
        </div>
      </el-col>
    </el-row>
    <div>
      <ul>
        <li v-for="file in files" :key="file.id">
          <a v-if="file.upFile" :href="file.upFile">Play Audio</a>
          <p>{{ file.label }}</p>
          <p>Severity A: {{ file.severity_A }}</p>
          <p>Severity B: {{ file.severity_B }}</p>
          <p>Severity C: {{ file.severity_C }}</p>
          <p>Severity D: {{ file.severity_D }}</p>
          <p>Handled: {{ file.handled }}</p>
          <p>Need Handle: {{ file.need_handle }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import LineChart from './components/LineChart'
import PieChart from './components/PieChart'
import TransactionTable from './components/TransactionTable'
import BoxCard from './components/BoxCard'
import ComplexTable from '@/views/table/complex-table'
// import MixChart from './components/Charts/MixChart'
// import ComplexTable from './components/complex_table.vue'

const lineChartData = {
  newVisitis: {
    expectedData: [17.52, 354.19, 90.17, 82.39],
    actualData: [17.89, 366.92, 92.54, 93.96]
  },
  messages: {
    expectedData: [200, 192, 120, 144, 160, 130, 140],
    actualData: [180, 160, 151, 106, 145, 150, 130]
  },
  purchases: {
    expectedData: [80, 100, 121, 104, 105, 90, 100],
    actualData: [120, 90, 100, 138, 142, 130, 130]
  },
  shoppings: {
    expectedData: [130, 140, 141, 142, 145, 150, 160],
    actualData: [120, 82, 91, 154, 162, 140, 130]
  }
}

// const MixChartData = {
//   newVisitis: {
//     expectedData: [100, 120, 161, 134, 105, 160, 165],
//     actualData: [120, 82, 91, 154, 162, 140, 145]
//   },
//   messages: {
//     expectedData: [200, 192, 120, 144, 160, 130, 140],
//     actualData: [180, 160, 151, 106, 145, 150, 130]
//   },
//   purchases: {
//     expectedData: [80, 100, 121, 104, 105, 90, 100],
//     actualData: [120, 90, 100, 138, 142, 130, 130]
//   },
//   shoppings: {
//     expectedData: [130, 140, 141, 142, 145, 150, 160],
//     actualData: [120, 82, 91, 154, 162, 140, 130]
//   }
// }

export default {
  name: 'DashboardAdmin',
  components: {
    LineChart,
    PieChart,
    TransactionTable,
    BoxCard,
    ComplexTable
    // MixChart
  },
  data: function() {
    return {
      lineChartData: lineChartData.newVisitis,
      // MixChartData: MixChartData.newVisitis
      files: []
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    handleSetLineChartData(type) {
      this.lineChartData = lineChartData[type]
      // this.MixChartData = MixChartData[type]
    },
    fetchData() {
      fetch('http://163.18.44.158:9000/data_view/?format=json')
        .then(response => response.json())
        .then(data => {
          this.files = data.results
        })
    }
  }
}
</script>

<style lang="scss" scoped>
.dashboard-editor-container {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  position: relative;

  .github-corner {
    position: absolute;
    top: 0px;
    border: 0;
    right: 0;
  }

  .chart-wrapper {
    background: #fff;
    padding: 32px 32px 0;
    margin-bottom: 32px;
  }
}

@media (max-width: 1024px) {
  .chart-wrapper {
    padding: 8px;
  }
}
</style>
