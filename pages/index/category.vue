<!--
 * @Author: error: git config user.name && git config user.email & please set dead value or install git
 * @Date: 2022-08-05 20:00:58
 * @LastEditors: error: git config user.name && git config user.email & please set dead value or install git
 * @LastEditTime: 2022-08-06 19:57:00
 * @FilePath: \idle\pages\index\category.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<!-- 分类 -->
<template>
	<view class="category-box">
		<!-- 三级分类 -->
		<three-catgory :categoryStyleId="categoryStyleId" v-if="categoryType === 4"></three-catgory>
		<!-- 二级分类 -->
		<two-catgory :categoryStyleId="categoryStyleId" v-if="categoryType === 3"></two-catgory>
		<!-- 一级分类-->
		<one-catgory :categoryStyleId="categoryStyleId" v-if="categoryType === 2"></one-catgory>
		<!--直接购买，点餐 -->
		<takeout-catgory :categoryStyleId="categoryStyleId" v-if="categoryType === 1"></takeout-catgory>
		<!-- 登录提示 -->
		<shopro-auth-modal v-if="authType"></shopro-auth-modal>
		<!-- <shopro-tabbar></shopro-tabbar> -->
	</view>
</template>

<script>
import takeoutCatgory from './category/takeout-catgory.vue';
import threeCatgory from './category/three-catgory.vue';
import twoCatgory from './category/two-catgory.vue';
import oneCatgory from './category/one-catgory.vue';
import { mapMutations, mapActions, mapState, mapGetters } from 'vuex';
export default {
	components: {
		takeoutCatgory,
		threeCatgory,
		twoCatgory,
		oneCatgory
	},
	data() {
		return {
			categoryType: 0, //1:快速购买,2:一级分类，3:二级分类，4:三级分类
			categoryStyleId: 0 //分类Id
		};
	},
	computed: {
		...mapGetters(['authType'])
	},
	onLoad() {
		this.getCategory();
	},
	methods: {
		/**
		 * 获取分类数据
		 *  type4:三级分类， type3:二级分类 ,type2:一级分类,type1:快速购买
		 */
		getCategory() {
			this.$http('category.info', {
				id: this.$Route.query.id ? this.$Route.query.id : 0
			}).then(res => {
				if (res.code === 1) {
					if (res.data?.type) {
						this.categoryType = Number(res.data.type);
						this.categoryStyleId = Number(res.data.id);
						uni.setNavigationBarTitle({
							title: res.data?.name
						});
					}
				}
			});
		}
	}
};
</script>

<style lang="scss">
.category-box {
	height: 100%;
	flex: 1;
	overflow: hidden;
}
</style>
