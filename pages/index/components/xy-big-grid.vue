<!--
 * @Author: error: git config user.name && git config user.email & please set dead value or install git
 * @Date: 2022-08-05 20:00:58
 * @LastEditors: error: git config user.name && git config user.email & please set dead value or install git
 * @LastEditTime: 2022-08-06 11:29:23
 * @FilePath: \idle\pages\index\components\xy-big-grid.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->

<template>
  <view class="flex-sb big-grid-wrap">
    <view v-for="(item, index) in list" :key="index">
      <view class="big-grid">
        <image
          :src="item.imgUrl"
          mode=""
          style="width: 240rpx; height: 120rpx"
        />
      </view>
      <view class="text-c mt10">{{ item.name }}</view>
    </view>
  </view>
</template>

<script>
export default {
  props: {
    list: {
      type: Array,
      default: () => {
        return [
          {
            imgUrl: "/static/images/empty_network.png",
            name: "居家",
          },
          {
            imgUrl: "/static/images/empty_network.png",
            name: "户外",
          },
        ];
      },
    },
  },
  data() {
    return {};
  },
};
</script>

<style lang="scss" scoped>
.big-grid-wrap{
  background: #fff;
  padding: 40rpx 80rpx 20rpx;
  margin-bottom: 10rpx;
  
}
  .big-grid{
    border: 1px solid #333;
    border-radius: 10rpx;
  }
</style>