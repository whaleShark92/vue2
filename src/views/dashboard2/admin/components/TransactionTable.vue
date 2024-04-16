<template>
  <div>
    <mallki class-name="mallki-text" text="病患資料" />
    <el-table :data="tableData" style="width: 100%;padding-top: 15px;">
      <el-table-column prop="no" width="180" />
      <el-table-column prop="date" width="180" />
      <!--      <el-table-column prop="no" label="No." width="180" />-->
      <!--      <el-table-column prop="date" label="Date" width="180" />-->
    </el-table>
  </div>
</template>

<script>
import { transactionList } from '@/api/remote-search'
import Mallki from '@/components/TextHoverEffect/Mallki.vue'

export default {
  components: { Mallki },
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
      tableData: [
        {
          no: '病歷號',
          date: '1234567'
        },
        {
          no: '性別',
          date: '男'
        },
        {
          no: '檢測時間',
          date: '2024-04/06 16:22:43'
        },
        {
          no: '出生年月日',
          date: '2003-12-23'
        },
        {
          no: '年齡',
          date: 20
        },
        {
          no: '科別',
          date: '復健科'
        }
      ]
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      transactionList().then(response => {
        this.list = response.data.items.slice(0, 8)
      })
    }
  }
}
</script>
