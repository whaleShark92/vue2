<template>
  <div>
    <mallki class-name="mallki-text" text="裝置狀態" />
    <br>
    <!--  <el-card class="box-card-component" style="margin-left:8px;">-->
    <!--    <div slot="header" class="box-card-header">-->
    <!--      <img src="./device.png" alt="">-->
    <!--    </div>-->
    <div class="image-container">
      <img src="./device.png" alt="Image Description">
    </div>
    <!--          <el-table-column label="Actions" align="center" width="230" class-name="small-padding fixed-width">-->
    <mallki class-name="mallki-text" text=" Collector gen3_v5" />
    <br>
    <router-link to="/dashboard3">
      <el-button type="success" @click="handleModifyStatus()">
        Console
      </el-button>
    </router-link>
    <router-link to="/dashboard2">
      <el-button type="success">
        Back
      </el-button>
    </router-link>
    <!--          </el-table-column>-->
  </div>
  <!--    </div>-->
  <!--  </el-card>-->
</template>

<script>
import { mapGetters } from 'vuex'
// import PanThumb from '@/components/PanThumb'
import Mallki from '@/components/TextHoverEffect/Mallki'

export default {
  components: { Mallki },
  filters: {
    statusFilter(status) {
      const statusMap = {
        success: 'success',
        pending: 'danger'
      }
      return statusMap[status]
    }
  },
  data() {
    return {
      statisticsData: {
        article_count: 1024,
        pageviews_count: 1024
      }
    }
  },
  methods: {
    handleModifyStatus() {
      // 调用 index.vue 中的 handleConnect 方法，切换组件
      this.$message({
        message: 'Attempt to connect',
        type: 'success'
      })
    }
  },
  computed: {
    ...mapGetters([
      'name',
      'avatar',
      'roles'
    ])
  }
}
</script>

<style scoped>
.image-container {
  width: 100%; /* 或其他您想要的寬度 */
  height: 0;
  padding-bottom: 75%; /* 這將設定圖片的高度為寬度的 75% */
  position: relative;
}

.image-container img {
  position: absolute;
  width: 100%;
  height: 100%;
  object-fit: cover; /* 這將確保圖片總是填滿容器，並保持其原始的寬高比 */
}
</style>
<style lang="scss">
.box-card-component {
  .el-card__header {
    padding: 0px !important;
  }
}
</style>
<style lang="scss" scoped>
.box-card-component {
  .box-card-header {
    position: relative;
    height: 220px;

    img {
      width: 100%;
      height: 100%;
      transition: all 0.2s linear;

      &:hover {
        transform: scale(1.1, 1.1);
        filter: contrast(130%);
      }
    }
  }

  .mallki-text {
    position: absolute;
    top: 0px;
    right: 0px;
    font-size: 20px;
    font-weight: bold;
  }

  .panThumb {
    z-index: 100;
    height: 70px !important;
    width: 70px !important;
    position: absolute !important;
    top: -45px;
    left: 0px;
    border: 5px solid #ffffff;
    background-color: #fff;
    margin: auto;
    box-shadow: none !important;

    ::v-deep .pan-info {
      box-shadow: none !important;
    }
  }

  .progress-item {
    margin-bottom: 10px;
    font-size: 14px;
  }

  @media only screen and (max-width: 1510px) {
    .mallki-text {
      display: none;
    }
  }
}
</style>
