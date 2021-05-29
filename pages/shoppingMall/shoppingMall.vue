<template>
	<view class="ShoppingMall">
		<uni-nav-bar fixed="true" class="status_title" color="#000000" statusBar="true" :title="title"></uni-nav-bar>
		<!-- search -->
		<view class="search">
			<view class="search-view">
				<text class="iconfont icon-search search-icon"></text>
				<text class="search-text">输入搜索内容</text>
			</view>
		</view>
		<!-- banner -->
		<view class="banner">
			<!-- 轮播 -->
			<uni-swiper-dot :info="swiperImg" :current="current" field="content" :mode="mode" class="swiper"
				:dotsStyles="dotsStyles">
				<swiper class="swiper-box" @change="changeSwiper">
					<swiper-item v-for="(item ,index) in swiperImg" :key="index">
						<view class="swiper-item">
							<image :src="item" mode="" lazy-load></image>
						</view>
					</swiper-item>
				</swiper>
			</uni-swiper-dot>
		</view>
		<!-- type_nav -->
		<address-nav :addressNav="type_nav"></address-nav>
		<!-- recommend -->
		<recommend :recommend="recommend" class="shop_recommend"></recommend>
		<view class="" style="width: 690rpx;height: 50rpx;"></view>
		<view class="tab">
			<view class="tab-item" v-for="(item,index) in tab" :key="index" @click="navTo(item.url)">
				<image :src="item.img" mode="heightFix" lazy-load></image>
				<text> {{item.text}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	import addressNav from '../../components/address-nav/address-nav.vue'
	import recommend from '../../components/recommend/recommend.vue'
	export default {
		components: {
			addressNav,
			recommend
		},
		data() {
			return {
				title: '商城',
				//banner
				swiperImg: [
					'../../static/image/shoppingMall/banner.png',
					'../../static/image/shoppingMall/banner.png'
				],
				none: true,
				current: 0,
				mode: 'round',
				swiperCurrent: 0,
				dotsStyles: {
					width: 8,
					height: 8,
					bottom: 13,
					backgroundColor: 'rgba(255, 255, 255,1)',
					border: '1px rgba(0, 0, 0, .3) solid',
					selectedBackgroundColor: 'rgba(254, 206, 10, 1)',
					selectedBorder: 'none'
				},
				//type_nav
				type_nav: [{
						img: '../../static/image/shoppingMall/HighlandBarleyWine.png',
						text: '青稞酒',
						url: 'url1'
					},
					{
						img: '../../static/image/shoppingMall/jerky.png',
						text: '肉干',
						url: 'url2'
					},
					{
						img: '../../static/image/shoppingMall/medicinalMaterials.png',
						text: '当地药材',
						url: 'url3'
					},
					{
						img: '../../static/image/shoppingMall/Accessories.png',
						text: '特色服饰',
						url: 'url4'
					}
				],
				recommend: {
					recommendTitleLeftImg: '../../static/image/shoppingMall/DiagonalBar1.png',
					recommendBack: '../../static/image/my/banner.png',
					type: '青海',
					detail: '青海省的特产有：旱獭皮，黑紫羔皮，藏刀，冬虫夏草，贝母，鹿茸，沙果，雪莲，柴杞（柴达木枸杞），青稞酒，羌活，西宁大黄，蕨麻，黑枸杞，红景天，秦艽等。',
					recommends: [{
							img: '../../static/image/index/bagroundImage.png',
							title: '青海特产黑果枸杞',
							price: 300,
							num: 305,
							recommendColor: '#FA3117',

						},
						{
							img: '../../static/image/index/commodity1.png',
							title: '青海特产藏牦牛肉',
							price: 300,
							num: 305,
							recommendColor: '#FA3117',

						},
						{
							img: '../../static/image/index/commodity2.png',
							title: '藏族特色冬虫夏草',
							price: 300,
							num: 305,
							recommendColor: '#FA3117',

						},
						{
							img: '../../static/image/index/commodity3.png',
							title: '藏族青稞酒',
							price: 300,
							num: 305,
							recommendColor: '#FA3117',
						},
					]
				},
				tab: [{
						img: '../../static/image/shoppingMall/index.png',
						text: '首页',
						url: '/pages/index/index'
					},
					{
						img: '../../static/image/shoppingMall/shopping.png',
						text: '环境教育',
						url: '/pages/my/my'
					},
					{
						img: '../../static/image/shoppingMall/dalou.png',
						text: '商城',
						url: '/pages/shoppingMall/shoppingMall'
					},
					{
						img: '../../static/image/shoppingMall/lanzi.png',
						text: '购物车',
						url: '/pages/my/my'
					},
					{
						img: '../../static/image/shoppingMall/my.png',
						text: '我的',
						url: '/pages/my/my'
					},

				]
			};
		},
		methods: {
			changeSwiper(e) {
				this.current = e.detail.current;
			},
			//tab跳转
			navTo(url) {
				// console.log(url);
				uni.reLaunch({
					url: url
				});
			}
		}
	}
</script>

<style lang="scss">
	.ShoppingMall {
		padding: 0 30rpx;

		.status_title {
			font-size: 34rpx;
			font-family: PingFang;
			font-weight: bold;
		}

		.search {
			width: 690rpx;
			height: 58rpx;
			// background-color: #0077AA;	
			padding: 20rpx 0 22rpx 0;

			.search-view {
				width: 100%;
				height: 100%;
				background-color: rgba(153, 153, 153, 0.3);
				border-radius: 29rpx;
				display: flex;
				justify-content: center;
				align-items: center;

				.search-icon {
					font-size: 40rpx;
				}

				.search-text {
					font-size: 24rpx;
					font-family: PingFang;
					font-weight: 400;
					color: #666666;
					line-height: 38rpx;
					margin-left: 7rpx;

				}
			}
		}

		//banner
		.banner {

			// margin-top: 15rpx;
			swiper {
				height: 280rpx;
			}

			.swiper {
				width: 690rpx;
				height: 280rpx;
				border-radius: 16rpx;
				overflow: hidden;
				position: relative;

				.swiper-item {
					width: 750rpx;
					height: 280rpx;

					image {
						width: 690rpx;
						height: 280rpx;
						display: block;
						box-sizing: border-box;
						border-radius: 6rpx;
					}
				}

			}
		}

		/deep/.recommend {
			margin-top: 128rpx;

			.title {
				margin-bottom: 47rpx;
			}
		}

		.tab {
			background-color: #FECE0A;

			text {
				font-size: 20rpx;
				font-family: PingFang;
				font-weight: 500;
				color: #FA3117;
				opacity: 0.8;
			}
		}
	}

	/* 修改第三方组件 */
	//导航栏
	/deep/ .uni-navbar--border.data-v-6bda1a90 {
		border: none !important;
	}
</style>
