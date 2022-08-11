<!--
 * @Author: error: git config user.name && git config user.email & please set dead value or install git
 * @Date: 2022-08-06 20:13:27
 * @LastEditors: error: git config user.name && git config user.email & please set dead value or install git
 * @LastEditTime: 2022-08-06 20:14:46
 * @FilePath: \idle\pages\index\index\city-select.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
  <view class="city-select">
    <u-index-list :scrollTop="scrollTop" v-if="type == 0">
      <view v-for="(item, index) in indexList" :key="index">
        <u-index-anchor :index="item" />
        <view class="list-cell"> 列表1 </view>
        <view class="list-cell"> 列表2 </view>
        <view class="list-cell"> 列表3 </view>
      </view>
    </u-index-list>
    <view v-else class="flex area">
      <view class="left-item">
        <view class="city-item" :class="index == curIndex?'selected-city':''" v-for="item,index in cityList" :key="index" @click="cityClick(index)">
          {{item.name}}
        </view>
      </view>
      <view class="right-item">
        <view class="area-item" v-for="item,index in cityList[curIndex].children" :key="index">
        {{item.name}}
      </view>
      </view>
      
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      type: 1,
      curIndex: 0,
      cityList: [
        {
          name: "杭州市",
          children: [
            {
              name: "上城区",
            },
            {
              name: "下城区",
            },
            {
              name: "下城区",
            },
            {
              name: "下城区",
            },
            {
              name: "下城区",
            },
            {
              name: "下城区",
            },
            {
              name: "下城区",
            },
            {
              name: "下城区",
            },
          ],
        },
        {
          name: "合肥市",
          children: [
            {
              name: "蜀山区",
            },
            {
              name: "滨湖区",
            },
          ],
        },
      ],
      scrollTop: 0,
      indexList: [
        "A",
        "B",
        "C",
        "D",
        "E",
        "F",
        "G",
        "H",
        "I",
        "J",
        "K",
        "L",
        "M",
        "N",
        "O",
        "P",
        "Q",
        "R",
        "S",
        "T",
        "U",
        "V",
        "W",
        "X",
        "Y",
        "Z",
      ],
    };
  },
  onPageScroll(e) {
    this.scrollTop = e.scrollTop;
  },
  methods:{
    cityClick(index){
      this.curIndex  = index
    }
  }
};
</script>

<style lang="scss" scoped>
.city-select{
  min-height: 100vh;
    background: #fff;
}
.area{
  height: 100vh;
  border: 1px solid #eee;
}
.left-item{
  width: 40%;
  height: 100%;
  border-right: 1px solid #eee;
  text-align: center;
}
.right-item{
  width: 60%;
  height: 100%;
}
.city-item{
  padding: 40rpx 10rpx;
  border-bottom: 1px solid #eee;
}
.area-item{
  padding: 10rpx 40rpx;
  border-bottom: 1px solid #eee;
}
.selected-city{
  font-weight: bold;
}
.list-cell {
  display: flex;
  box-sizing: border-box;
  width: 100%;
  padding: 10px 24rpx;
  overflow: hidden;
  color: #323233;
  font-size: 14px;
  line-height: 24px;
  background-color: #fff;
}

.anchor-text {
  color: red;
}
</style>