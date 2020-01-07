<template>
  <div class="header"
       @click="showDetail">
    <div class="content-wrapper">
      <!-- 左侧图像 -->
      <div class="avatar">
        <img width="64"
             height="64"
             :src="seller.avatar"
             alt="">
      </div>
      <!-- 商家详情 -->
      <div class="content">
        <!-- 标题 -->
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <!-- 商家描述 -->
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <!-- 支持优惠情况 -->
        <div v-if="seller.supports"
             class="support">
          <support-ico :size=1
                       :type='seller.supports[1].type'></support-ico>
          <span class="text">{{seller.supports[1].description}}</span>
        </div>
      </div>
      <!-- 支持优惠个数 -->
      <div class="support-count"
           v-if="seller.supports">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar"
           width="100%"
           height="100%"
           alt="">
    </div>
  </div>
</template>
<script type='text/ecmascript-6'>
import SupportIco from 'components/support-ico/support-ico'
export default {
  name: 'v-header',
  props: {
    seller: {
      type: Object,
      default () {
        return {}
      }
    }
  },
  methods: {
    showDetail () {
      // 防止重复创建
      this.headerDetailComp = this.headerDetailComp || this.$createHeaderDetail({
        $props: {
          seller: 'seller'
        }
      })
      this.headerDetailComp.show()
    }
  },
  components: {
    SupportIco
  }
}
</script>
<style lang='stylus' rel='stylesheet/stylus'>
@import '~common/stylus/mixin';
@import '~common/stylus/variable';

.header {
  position: relative;
  overflow: hidden;
  color: $color-white;
  background: $color-background-ss;

  .content-wrapper {
    position: relative;
    display: flex;
    align-items: center;
    padding: 24px 12px 18px 24px;

    .avatar {
      // 固定占据64px 不随剩余空间放大缩小
      flex: 0 0 64px;
      width: 64px;
      margin-right: 16px;

      img {
        border-radius: 2px;
      }
    }

    .content {
      // 占据所有剩余空间
      flex: 1;

      .title {
        display: flex;
        // 垂直居中
        align-items: center;
        margin-bottom: 8px;

        .brand {
          width: 30px;
          height: 18px;
          // 根据dpr（像素比）选择性加载图片
          bg-image('brand');
          // 背景的长宽
          background-size: 30px 18px;
          background-repeat: no-repeat;
        }

        .name {
          margin-left: 6px;
          font-size: $fontsize-large;
          font-weight: bold;
        }
      }

      .description {
        margin-bottom: 8px;
        line-height: 12px;
        font-size: $fontsize-small;
      }

      .support {
        display: flex;
        align-items: center;

        .support-ico {
          margin-right: 4px;
        }

        .text {
          line-height: 12px;
          font-size: $fontsize-small-s;
        }
      }
    }

    .support-count {
      position: absolute;
      right: 12px;
      bottom: 14px;
      display: flex;
      align-items: center;
      padding: 0 8px;
      height: 24px;
      line-height: 24px;
      text-align: center;
      border-radius: 14px;
      background: $color-background-sss;

      .count {
        font-size: $fontsize-small-s;
      }

      .icon-keyboard_arrow_right {
        margin-left: 2px;
        line-height: 24px;
        font-size: $fontsize-small-s;
      }
    }
  }

  .bulletin-wrapper {
    position: relative;
    display: flex;
    align-items: center;
    height: 28px;
    line-height: 28px;
    padding: 0 8px;
    background: $color-background-sss;

    .bulletin-title {
      flex: 0 0 22px;
      width: 22px;
      height: 12px;
      margin-right: 4px;
      bg-image('bulletin');
      background-size: 22px 12px;
      background-repeat: no-repeat;
    }

    .bulletin-text {
      flex: 1;
      // 文字超出隐藏
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      font-size: $fontsize-small-s;
    }

    .icon-keyboard_arrow_right {
      flex: 0 0 10px;
      width: 10px;
      font-size: $fontsize-small-s;
    }
  }

  .background {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: -1;
    // 调整背景模糊度
    filter: blur(10px);
  }
}
</style>
