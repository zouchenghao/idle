<template>
  <view class="xy-filter">
    <u-dropdown ref="uDropdown" class="xy-filter-uDropdown" border-radius="20">
      <u-dropdown-item
        v-model="params.sort"
        :title="params.sort"
        :options="sortList"
        @change="sortChange"
      ></u-dropdown-item>
      <u-dropdown-item :title="params.area">
        <view class="slot-content">
          <view class="content m-bc-fff flex font12">
            <scroll-view class="flex-1 list-1">
              <view class="list-1-item item">小区</view>
              <view class="list-1-item item">附近</view>
              <view class="list-1-item item">地铁</view>
            </scroll-view>
            <scroll-view scroll-y="true" class="flex-1 list-2">
              <view class="list-2-item item">不限</view>
              <view class="list-2-item item">上城区</view>
              <view class="list-2-item item">上城区</view>
              <view class="list-2-item item">上城区</view>
              <view class="list-2-item item">上城区</view>
              <view class="list-2-item item">上城区</view>
              <view class="list-2-item item">上城区</view>
              <view class="list-2-item item">上城区</view>
              <view class="list-2-item item">上城区</view>
              <view class="list-2-item item">上城区</view>
              <view class="list-2-item item">上城区</view>
              <view class="list-2-item item">上城区</view>
              <view class="list-2-item item">上城区</view>
            </scroll-view>
            <scroll-view class="flex-1 list-3">
              <view class="list-3-item item">不限</view>
              <view class="list-3-item item">上城区</view>
            </scroll-view>
          </view>
        </view>
      </u-dropdown-item>
      <u-dropdown-item title="价格">
        <view class="slot-content">
          <view class="m-bc-fff font12 price-content pl10 pr10 pb20">
            <view>价格范围（元）</view>
            <view class="flex-sac mt10 pl20 pr20">
              <input
                class="_input"
                v-model="params.lowPrice"
                type="number"
                placeholder="最低价"
              />
              <view>——</view>
              <input
                type="number"
                class="_input"
                v-model="params.highPrice"
                placeholder="最高价"
              />
            </view>
            <view class="flex-sac flex-wrap">
              <u-button
                throttle-time="0"
                @click="params.activeSelectPriceArea = index"
                v-for="(item, index) in priceList"
                :key="index"
                shape="circle"
                :type="params.activeSelectPriceArea === index ? 'primary' : ''"
                class="_button"
                >{{ item.value }}</u-button
              >
            </view>
            <view class="flex mt20">
              <u-button
                type="primary"
                plain
                @click="resetParams"
                style="width: 200rpx; height: 60rpx"
                >重置</u-button
              >
              <u-button
                type="primary"
                @click="closeDropdown"
                style="width: 200rpx; height: 60rpx"
                >确定</u-button
              >
            </view>
          </view>
        </view>
      </u-dropdown-item>
    </u-dropdown>
  </view>
</template>

<script>
export default {
  props: {
    tabListParams: {
      type: Object,
      default: () => {},
    },
    tabIndex: {
      type: Number,
      default: 0,
    },
  },
  watch: {
    tabListParams(v) {
      this.params = v;
    },
    tabIndex(v) {
      console.log(v);
      if (v != 100) {
        this.$refs["uDropdown"].menuClick(v);
      }
    },
  },
  data() {
    return {
      priceList: [
        { value: "200元以下" },
        { value: "200元以下" },
        { value: "200元以下" },
        { value: "200元以下" },
        { value: "200元以下" },
        { value: "200元以下" },
        { value: "200元以下" },
        { value: "200元以下" },
      ],
      params: {
        sort: "排序",
        area: "区域",
        price: "价格",
        activeSelectPriceArea: "",
      },
      sortList: [
        {
          label: "默认排序",
          value: "排序",
        },
        {
          label: "价格降序",
          value: "价格降序",
        },
        {
          label: "价格升序",
          value: "价格升序",
        },
        {
          label: "最近更新",
          value: "最近更新",
        },
        {
          label: "离我最近",
          value: "离我最近",
        },
      ],
    };
  },
  methods: {
    resetParams() {
      this.params.lowPrice = "";
      this.params.highPrice = "";
      this.params.activeSelectPriceArea = "";
    },
    closeDropdown() {
      this.$refs.uDropdown.close();
    },
    sortChange(e) {
      this.$emit("tabList", this.params);
      console.log(e);
    },
  },
};
</script>

<style lang="scss" scoped>
// #ifdef H5
/deep/ .xy-filter-uDropdown {
  padding: 0 100rpx;
}
// #endif
// #ifdef MP-WEIXIN
/deep/ .xy-filter-uDropdown > view {
  padding: 0 100rpx;
}
// #endif
.content {
  height: 400rpx;
  > view {
    height: 100%;
    overflow-y: scroll;
  }
  .item {
    padding: 20rpx 15rpx;
    border-top: 1px solid #eee;
  }
  .list-1 {
    border-right: 1px solid #eee;
    .list-1-item {
    }
  }
  .list-3 {
    border-left: 1px solid #eee;
  }
}
/deep/._input {
  border: 1px solid #eee;
  width: 200rpx;
  height: 60rpx;
  border-radius: 40rpx;
  padding: 10rpx;
  text-align: center;
  font-size: 24rpx;
}
/deep/._button {
  margin-top: 20rpx;
  min-width: 180rpx;
  height: 50rpx;
  font-size: 24rpx;
}
/deep/.u-hairline-border::after{
border-color: #eee
}
uni-button {
  background-color: #fff;
}
</style>