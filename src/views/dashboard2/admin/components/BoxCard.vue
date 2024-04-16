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

    <div style="position:relative;">
      <!--      <pan-thumb :image="avatar" class="panThumb" />-->
      <br>
      <mallki class-name="mallki-text" text=" Collector gen3_v5" />

      <div style="padding-top:35px;" class="progress-item">
        <span>裝置連線狀態：</span>
        <el-progress :percentage="100" status="success" />
        <br>
      </div>
      <div class="progress-item">
        <span>剩餘電量：</span>
        <el-progress :percentage="50" />
        <br>
      </div>

    </div>
  </div>
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
