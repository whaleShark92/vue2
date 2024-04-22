<template>
  <div>
    <mallki class-name="mallki-text" text="病患資料" />
    <bar-chart :data="chartData" />
    <!--    <el-table :data="tableData" style="width: 100%;padding-top: 15px;">-->
    <!--      <el-table-column prop="no" width="180" />-->
    <!--      <el-table-column prop="date" width="180" />-->
    <!--      &lt;!&ndash;      <el-table-column prop="no" label="No." width="180" />&ndash;&gt;-->
    <!--      &lt;!&ndash;      <el-table-column prop="date" label="Date" width="180" />&ndash;&gt;-->
    <div>
      <el-table :data="chartData" border>
        <!--        <el-table-column prop="label" label="label"/>-->
        <!--        <el-table-column prop="upFile" label="upFile"/>-->
        <el-table-column prop="severity_A" label="severity_A" />
        <el-table-column prop="severity_B" label="severity_B" />
        <el-table-column prop="severity_C" label="severity_C" />
        <el-table-column prop="severity_D" label="severity_D" />
        <!--          <el-table-column prop="handled" label="handled" :formatter="formatBoolean" />-->
        <!--          <el-table-column prop=" need_handle" label="need_handle" :formatter="formatBoolean" />-->
      </el-table>
    </div>
    <!--    </el-table>-->
  </div>
</template>

<script>
// import { transactionList } from '@/api/remote-search'
import Mallki from '@/components/TextHoverEffect/Mallki.vue'
import BarChart from '@/views/dashboard2/admin/components/BarChart.vue'

export default {
  components: { BarChart, Mallki },
  filters: {
    statusFilter(status) {
      const statusMap = {
        success: 'success',
        pending: 'danger'
      }
      return statusMap[status]
    },
    orderNoFilter(str) {
      return str.substring(0, 30)
    }
  },
  data() {
    return {
      list: null,
      // files: null,
      chartData: null
      // tableData: [
      //   {
      //     no: '病歷號',
      //     date: '1234567'
      //   },
      //   {
      //     no: '性別',
      //     date: '男'
      //   },
      //   {
      //     no: '檢測時間',
      //     date: '2024-04-06 16:22:43'
      //   },
      //   {
      //     no: '出生年月日',
      //     date: '2003-12-23'
      //   },
      //   {
      //     no: '年齡',
      //     date: 20
      //   },
      //   {
      //     no: '科別',
      //     date: '復健科'
      //   }
      // ]
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      fetch('http://163.18.44.158:9000/data_view/?format=json')
        .then(response => response.json())
        .then(data => {
          this.chartData = data.results.slice(0, 2)
        })
    }
  }
  // computed: {
  //   chartData() {
  //     // 取得前兩筆資料
  //     return this.files ? this.files.slice(0, 2) : []
  //   }
  // }
}
</script>
