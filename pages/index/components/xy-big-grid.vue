<template>
  <view class="flex-sb">
    <view v-for="(item, index) in list" :key="index">
      <view>
        <image
          :src="item.imgUrl"
          mode=""
          style="width: 180rpx; height: 100rpx"
        />
      </view>
      <view>{{ item.name }}</view>
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

<style>
</style>