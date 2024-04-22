<template>
  <div class="dashboard-editor-container">
    <div>
      <el-table :data="files" border>
        <el-table-column prop="person_id" label="ID" />
        <el-table-column prop="name" label="Name" />
        <el-table-column prop="gender" label="Gender" />
        <el-table-column prop="age" label="Age" />
      </el-table>
    </div>
  </div>
</template>

<script>

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

export default {
  name: 'DashboardAdmin',
  components: {
  },
  data() {
    return {
      lineChartData: lineChartData.newVisitis,
      files: []
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    handleSetLineChartData(type) {
      this.lineChartData = lineChartData[type]
    },
    fetchData() {
      fetch('http://163.18.44.158:9000/person_view/?format=json')
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
