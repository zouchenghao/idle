<!-- 首页 -->
<template>
  <view class="home-wrap u-m-b-20">
    <!-- 空白页 -->
    <!-- #ifdef APP-PLUS -->
    <u-no-network @retry="init"></u-no-network>
    <!-- #endif -->
    <shopro-empty
      v-if="!hasTemplate"
      :image="$IMG_URL + '/imgs/empty/template_empty.png'"
      tipText="暂未找到模板，请前往装修~"
    >
    </shopro-empty>

    <view v-else-if="isConnected && isRefresh" class="content-box">
      <!-- 选择城市 -->
      <!-- 导航栏 -->
      <home-head
        v-if="headSwiperList && headSwiperList.length"
        :isScorll="isScorll"
        borderRadius="0"
        :navTitle="initShop.name"
        :list="headSwiperList"
      ></home-head>
      <!-- 固定大模块 -->
      <!-- <xy-big-grid></xy-big-grid> -->
      <!-- 自定义模块 -->
      <!-- <view class="template-box">
        <block v-for="(item, index) in homeTemplate" :key="item.id"> -->
          <!-- 轮播 -->
          <!-- <sh-banner v-if="item.type === 'banner' && index !== 0" :Px="item.content.x" :Py="item.content.y"
						:borderRadius="item.content.radius" :height="item.content.height" :list="item.content.list">
					</sh-banner> -->

          <!-- 搜索 -->
          <!-- <sh-search v-if="item.type === 'search'"></sh-search> -->

          <!-- 滑动宫格 -->
          <!-- <sh-grid-swiper v-if="item.type === 'menu'" :list="item.content.list"
						:oneRowNum="item.content.style"></sh-grid-swiper> -->

          <!-- 推荐商品 -->
          <!-- <sh-hot-goods v-if="item.type === 'goods-list' || item.type === 'goods-group'"
						:detail="item.content"></sh-hot-goods> -->
          <!-- 广告魔方 -->
          <!-- <sh-adv v-if="item.type === 'adv'" :detail="item.content"></sh-adv> -->
          <!-- 优惠券 -->
          <!-- <sh-coupon v-if="item.type === 'coupons'" :detail="item.content"></sh-coupon> -->
          <!-- 秒杀-->
          <!-- <sh-seckill v-if="item.type === 'seckill'" :detail="item.content"></sh-seckill> -->
          <!-- 拼团 -->
          <!-- <sh-groupon v-if="item.type === 'groupon'" :detail="item.content"></sh-groupon> -->
          <!-- 富文本 -->
          <!-- <sh-richtext v-if="item.type === 'rich-text'" :richId="item.content.id"></sh-richtext> -->
          <!-- 功能标题 -->
          <!-- <sh-title-card v-if="item.type === 'title-block'" :title="item.content.name"
						:bgImage="item.content.image" :titleColor="item.content.color"></sh-title-card> -->
          <!-- 直播 -->
          <!-- #ifdef MP-WEIXIN -->
          <!-- <sh-live v-if="item.type === 'live' && HAS_LIVE" :detail="item.content"></sh-live> -->
          <!-- #endif -->
        <!-- </block>
      </view> -->

      <!-- 分类选项卡 styleType 1 瀑布流 2 正常流-->
      <sh-category-tabs
      id="category"
        v-if="
          hackReset &&
          categoryTabsData &&
          categoryTabsData.category_arr &&
          categoryTabsData.category_arr.length
        "
        :enable="enable"
        :styleType="1"
        :tabsList="categoryTabsData.category_arr"
        @scrollToTop="pageScroll"
      >
      </sh-category-tabs>
      <!-- 登录提示 -->
      <shopro-auth-modal></shopro-auth-modal>
      <!-- 悬浮按钮 -->
      <!-- <shopro-float-btn></shopro-float-btn> -->
      <!-- 连续弹窗提醒 -->
      <shopro-notice-modal v-if="!showPrivacy && isLogin"></shopro-notice-modal>
      <!-- 隐私协议 -->
      <!-- #ifdef APP-PLUS -->
      <privacy-modal
        v-if="initShop && initShop.name"
        v-model="showPrivacy"
      ></privacy-modal>
      <!-- #endif -->
      <!-- #ifdef H5 -->
      <view class="tabbar-hack" style="height: 120rpx; width: 100%"></view>
      <!-- #endif -->
    </view>
    <!-- <shopro-tabbar></shopro-tabbar> -->
  </view>
</template>

<script>
import shBanner from "./components/sh-banner.vue";
import shGridSwiper from "./components/sh-grid-swiper.vue";
import shHotGoods from "./components/sh-hot-goods.vue";
import shAdv from "./components/sh-adv.vue";
import shCoupon from "./components/sh-coupon.vue";
import shSeckill from "./components/sh-seckill.vue";
import shGroupon from "./components/sh-groupon.vue";
import shRichtext from "./components/sh-richtext.vue";
import shTitleCard from "./components/sh-title-card.vue";
import shSearch from "./components/sh-search.vue";
import shCategoryTabs from "./components/sh-category-tabs.vue";
import xyBigGrid from "./components/xy-big-grid.vue";

import privacyModal from "./index/privacy-modal.vue";
import homeHead from "./index/home-head.vue";

// #ifdef MP-WEIXIN
import { HAS_LIVE } from "@/env";
import shLive from "./components/sh-live.vue";
// #endif

import { mapMutations, mapActions, mapState, mapGetters } from "vuex";
import XyBigGrid from "./components/xy-big-grid.vue";
export default {
  components: {
    shBanner,
    shGridSwiper,
    shGroupon,
    shHotGoods,
    shAdv,
    shCoupon,
    shSeckill,
    shRichtext,
    shTitleCard,
    shSearch,
    shCategoryTabs,
    xyBigGrid,

    privacyModal,
    homeHead,

    // #ifdef MP-WEIXIN
    shLive,
    XyBigGrid,
    // #endif
  },
  data() {
    return {
      // #ifdef MP-WEIXIN
      HAS_LIVE: HAS_LIVE,
      // #endif
      isRefresh: true,

      enable: false, //是否开启吸顶。
      isConnected: true, //是否有网
      showPrivacy: false, //协议
      isScorll: false,
      hackReset: true,
    };
  },
  computed: {
    ...mapGetters(["initShop", "homeTemplate", "hasTemplate", "isLogin"]),
    // 头部模块数据
    headSwiperList() {
      if (this.homeTemplate?.length) {
        return this.homeTemplate[0]?.content?.list;
      }
    },
    // 分类选项卡数据
    categoryTabsData() {
      if (this.homeTemplate?.length) {
        return this.homeTemplate[this.homeTemplate.length - 1]?.content;
      }
    },
  },
  onPullDownRefresh() {
    this.init();
  },
  onPageScroll(e) {
    this.isScorll = e.scrollTop > 100 ? true : false;
  },
  onShow() {
    let that = this;
    this.enable = true;
    this.isLogin && this.getCartList();
    // 网络变化检测
    uni.onNetworkStatusChange((res) => {
      this.isConnected = res.isConnected;
      res.isConnected && this.init();
    });
  },
  onHide() {
    this.hackReset = false;
    this.$nextTick(() => {
      this.hackReset = true;
    });
    this.enable = false;
  },
  async onLoad() {
    
    // #ifdef APP-VUE
    // app隐私协议弹窗
    if (!plus.runtime.isAgreePrivacy()) {
      this.showPrivacy = true;
      this.showNoticeModal = false;
    }
    // #endif
  },
  methods: {
    ...mapActions(["appInit", "getTemplate", "getCartList"]),
    // 初始化
    init() {
      this.isRefresh = false;
      return Promise.all([this.getTemplate()]).then(() => {
        uni.stopPullDownRefresh();
        this.isRefresh = true;
      });
    },
    pageScroll() {
      // const query = uni.createSelectorQuery().in(this);
      // query.select('#category').boundingClientRect(data => {
      //   console.log("得到布局位置信息" + JSON.stringify(data));
      //   console.log("节点离页面顶部的距离为" + data.top);
      // }).exec()
      // return
      //吸顶筛选
      uni.pageScrollTo({
        scrollTop: 500,
        duration: 100,
      });
    },
  },
};
</script>

<style lang="scss"></style>
