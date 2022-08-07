<!--
 * @Author: error: git config user.name && git config user.email & please set dead value or install git
 * @Date: 2022-08-06 20:13:27
 * @LastEditors: error: git config user.name && git config user.email & please set dead value or install git
 * @LastEditTime: 2022-08-06 20:14:46
 * @FilePath: \idle\pages\index\index\city-select.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
  <view>
    <u-index-list :scrollTop="scrollTop">
      <view v-for="(item, index) in indexList" :key="index">
        <u-index-anchor :index="item" />
        <view class="list-cell"> 列表1 </view>
        <view class="list-cell"> 列表2 </view>
        <view class="list-cell"> 列表3 </view>
      </view>
    </u-index-list>
  </view>
</template>

<script>
export default {
  data() {
    return {
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
};
</script>

<style lang="scss" scoped>
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