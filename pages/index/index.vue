<template>
	<view class="index">
		<!-- 这里是状态栏 -->
		<!-- <view class="status_bar"> -->
		<!-- 这里是状态栏 -->
		<!-- </view> -->
		<!-- <view class="status_title"> {{title}}</view> -->
		<uni-nav-bar fixed="true" class="status_title" color="#79C2EF" statusBar="true">
			<view slot="left" style="margin-left:20rpx;font-weight: bold;">{{ title }}</view>
		</uni-nav-bar>
		<!-- 搜索 -->
		<view class="search" @click="searchView">
			<view class="left">
				<text class="iconfont icon-address address-icon"></text>
				<text class="address">{{ currentAddress }}</text>
			</view>
			<view class="right">
				<view class="search-view">
					<view class="">
						<text class="iconfont icon-search search-icon"></text>
						<text class="search-text">输入搜索内容</text>
					</view>
				</view>
				<!-- <uni-search-bar radius=29 bgColor="rgba(153, 153, 153, 0.3)" v-model="search" clearButton="auto"
					cancelButton="auto" @input="searchView">
					<uni-icons slot="searchIcon" color="#999999" size="20" type="search" />
				</uni-search-bar> -->
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
		<!-- address-nav -->
		<view class="address-nav">
			<view class="address-nav-item" v-for="(item,index) in addressNav" :key="index"
				@click="address_nav_to(item)">
				<view class="img">
					<image :src="item.img" mode="widthFix"></image>
				</view>
				<view class="text">
					<text>{{ item.text }}</text>
				</view>
			</view>
		</view>
		<!-- detail-box -->
		<view class="detail-box" v-for="(item,index) in detailBox" :key="index">
			<view class="header">
				<view class="left">
					<view class="f-row">
						<view class="" style="width:40rpx;height: 40rpx;">
							<!-- <image src="../../static/image/index/组%202@2x(4).png" mode="widthFix"></image> -->
							<image :src="item.logo" mode="widthFix" lazy-load></image>
						</view>
						<view class="" style="margin-left: 12rpx; font-weight: bold;line-height: 38rpx;">
							{{ item.title }}
						</view>
					</view>
					<view class="s-row">
						<text>{{item.deatil}}</text>
					</view>
				</view>
				<view class="right" @click="detail_box_to(item)">
					<text>立即预约</text>
				</view>
			</view>
			<view class="" style="width: 690rpx;height:520rpx;">
				<view class="img">
					<view class="img-item">
						<view class="">
							<text class="iconfont icon-address" style="margin-right: 6rpx;"></text>
							<text class="address">{{ item.address }}</text>
						</view>
						<view class="">
							<text>报名中&nbsp;&nbsp;&nbsp;{{item.date}}</text>
						</view>
					</view>
					<image class="back" :src="item.back" mode="" lazy-load></image>
				</view>
				<view class="body">
					<view class="f-r">
						<view class="left">
							<text>(已成团){{ item.dateTime }}</text>
							<text>|</text>
							<text>{{item.address}}</text>
						</view>
						<view class="right">
							<text style="width:44rpx;font-size: 22rpx;font-weight: 400;">热度</text>
							<sunui-star :defaultStar="item.star" maxStar="5" :starSize='starConfig.starSize'
								:isTips="starConfig.isTips" type disabledStar @changeStar="changeStar"
								class='sunui-star' />
						</view>
					</view>
					<view class="s-r">
						<text class="f">
							<text style="color:#1961B6;font-size: 22rpx;font-weight: bold;">￥</text>
							<text
								style="color:#1961B6;font-size: 40rpx;font-weight: bold;margin-right: 9rpx;">{{ item.price }}</text>
							元起
						</text>
						<text class="s">{{ item.dateTimeDeatil }}</text>
						<text class="t">{{ item.time }}</text>
					</view>
					<view class="t-r">
						<view class="commin-text"
							style="max-width: 340rpx;display: -webkit-box;-webkit-box-orient: vertical;-webkit-line-clamp: 1;overflow: hidden;box-sizing: border-box;padding: 0 10rpx;"
							v-for="(tuijian,i) in item.tuijians" :key="i">{{ tuijian.text }}</view>
					</view>
				</view>
			</view>
		</view>
		<!-- 精品推荐-->
		<view class="recommend">
			<view class="title">
				<image :src="recommend.recommendTitleLeftImg" mode="" lazy-load></image>
				<text>特色商品推荐 </text>
				<image :src="recommend.recommendTitleLeftImg" mode="" lazy-load></image>
			</view>
			<view class="body">
				<view class="f-r">
					<view class="f-r-item">
						<view class=""><text>{{recommend.type}}特色</text><text>推荐</text></view>
						<view class="">
							<text>{{recommend.detail}}</text>
						</view>
					</view>
					<image class="back" :src="recommend.recommendBack" mode="" lazy-load></image>
				</view>
				<view class="s-r">
					<view class="s-r-item" v-for="(item,index) in recommend.recommends" :key="index"
						@click="recommend_detail_to(item)">
						<image :src="item.img" mode="" lazy-load></image>
						<view class="name"><text>{{item.title}}</text></view>
						<view class="price">
							<view class=""><text style="font-size: 22rpx;margin-right: 13rpx;" :style="{color:item.recommendColor}">￥</text><text
									style="margin-right: 5rpx;" :style="{color:item.recommendColor}">{{ item.price }}</text>元
							</view>
							<view class=""><text>已售</text>{{item.num}}</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="tab-top" v-if="isTop" style="">
		</view>
		<view class="tab" :class="isTop?'tabs':''">
			<view class="tab-item" v-for="(item,index) in tab" :key="index" @click="navTo(item.url)"
				:class="isTop?'tab-items':''">
				<image :src="item.img" mode="heightFix" lazy-load></image>
				{{item.text}}
			</view>
		</view>
	</view>
</template>

<script>
	import sunuiStar from '../../components/sunni-star/sunni-star.vue'
	export default {
		components: {
			sunuiStar
		},
		data() {
			return {
				isTop: false,
				title: '云享自然',
				currentAddress: '北京',
				search: '',
				swiperImg: [
					'../../static/image/index/banner6.png',
					'../../static/image/index/banner6.png'
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
					selectedBackgroundColor: 'rgba(121, 194, 239, 1)',
					selectedBorder: 'none'
				},
				starConfig: {
					defaultStar: 2,
					maxStar: 5,
					starSize: '22rpx',
					isTips: true,
					type: 'love'
				},
				addressNav: [{
						img: '../../static/image/index/logo1.png',
						text: '三江源国家公园',
						url: 'url1'
					},
					{
						img: '../../static/image/index/logo2.png',
						text: '祁连山国家公园',
						url: 'url2'
					},
					{
						img: '../../static/image/index/logo1.png',
						text: '三江源国家公园',
						url: 'url3'
					},
					{
						img: '../../static/image/index/logo1.png',
						text: '三江源国家公园',
						url: 'url4'
					}
				],
				detailBox: [{
						logo: '../../static/image/index/logo1.png',
						title: '三江源国家公园',
						deatil: '炎黄子孙孜孜不倦寻觅的母亲河源头',
						address: '江苏 盐城',
						date: '2021-4-30',
						dateTime: '4月30日',
						addName: '黄河源园区',
						price: '5500',
						dateTimeDeatil: '2021年4月30日',
						time: '七天七夜',
						back: '../../static/image/index/SanjiangyuanNationalPark.png',
						star: 5,
						tuijians: [{
							text: '2-6月合适'
						}, {
							text: '中国野生兽类能见度最高的区域'
						}]
					},
					{
						logo: '../../static/image/index/logo2.png',
						title: '祁连山国家公园',
						deatil: '炎黄子孙孜孜不倦寻觅的母亲河源头',
						address: '江苏 盐城',
						date: '2021-4-30',
						dateTime: '4月30日',
						addName: '黄河源园区',
						price: '5500',
						dateTimeDeatil: '2021年4月30日',
						time: '七天七夜',
						back: '../../static/image/index/QilianMountainNationalPark.png',
						star: 3,
						tuijians: [{
							text: '2-6月合适',

						}, {
							text: '中国野生兽类能见度最高的区域',
						}]
					},
				],
				recommend: {
					recommendTitleLeftImg:'../../static/image/index/Diagonal.png',
					recommendBack: '../../static/image/my/banner.png',
					type: '青海',
					detail: '青海省的特产有：旱獭皮，黑紫羔皮，藏刀，冬虫夏草，贝母，鹿茸，沙果，雪莲，柴杞（柴达木枸杞），青稞酒，羌活，西宁大黄，蕨麻，黑枸杞，红景天，秦艽等。',
					recommends: [{
							img: '../../static/image/index/bagroundImage.png',
							title: '青海特产黑果枸杞',
							price: 300,
							num: 305,
							recommendColor:'#1961B6',

						},
						{
							img: '../../static/image/index/commodity1.png',
							title: '青海特产藏牦牛肉',
							price: 300,
							num: 305,
							recommendColor:'#1961B6',

						},
						{
							img: '../../static/image/index/commodity2.png',
							title: '藏族特色冬虫夏草',
							price: 300,
							num: 305,
							recommendColor:'#1961B6',

						},
						{
							img: '../../static/image/index/commodity3.png',
							title: '藏族青稞酒',
							price: 300,
							num: 305,
							recommendColor:'#1961B6',

						},
					]
				},
				tab: [{
						img: '../../static/image/index/index.png',
						text: '首页',
						url: '/pages/index/index'
					},
					{
						img: '../../static/image/index/car.png',
						text: '环境教育',
						url: '/pages/my/my'
					},
					{
						img: '../../static/image/index/shop.png',
						text: '商城',
						url: '/pages/shoppingMall/shoppingMall'
					},
					{
						img: '../../static/image/index/shop_car.png',
						text: '购物车',
						url: '/pages/my/my'
					},
					{
						img: '../../static/image/index/my.png',
						text: '我的',
						url: '/pages/my/my'
					},

				]

			}
		},

		// onReady() {
		// 	uni.getSystemInfo({
		// 		success: e => {
		// 			console.log(e)
		// 			if (e.model == 'iPhone X' || e.model == 'iPhone XR' || e.model == 'iPhone XS Max') {
		// 				this.isTop = true;
		// 			} else {
		// 				this.isTop = false;
		// 			}
		// 		}
		// 	})
		// },
		methods: {
			changeSwiper(e) {
				this.current = e.detail.current;
			},
			changeStar() {

			},
			//tab跳转
			navTo(url) {
				// console.log(url);
				uni.reLaunch({
					url: url
				});
			},
			//搜索框发生变化
			searchView() {
				console.log(this.search)
			},
			//地址导航跳转
			address_nav_to(e) {
				console.log(e.url)
			},
			//预约
			detail_box_to(item) {
				console.log(item);
			},
			//精品详情
			recommend_detail_to(item) {
				console.log(item);
			}

		}
	}
</script>

<style lang="scss" scoped>
	.index {
		box-sizing: border-box;
		padding: 0 30rpx;
		font-weight: 400;

		.status_title {
			font-size: 34rpx;
			color: $cloud-enjoy-nature-color;
		}

		//搜索
		.search {
			width: 690rpx;
			height: 118rpx;
			// background-color: #007AFF;
			box-sizing: border-box;
			display: flex;
			padding: 0;

			.left {
				width: 110rpx;
				height: 118rpx;
				// background-color: #55A532;
				display: flex;
				align-items: center;

				.address-icon {
					font-size: 40rpx;
					box-sizing: border-box;
					padding-right: 6rpx;
					color: $index-font-color-one;
				}

				.address {
					font-size: 24rpx;
					color: $index-font-color-one;

				}

			}

			.right {
				width: 580rpx;
				height: 116rpx;
				// background-color: #0086B3;
				box-sizing: border-box;
				padding: 30rpx 0;

				.search-view {
					width: 580rpx;
					height: 58rpx;
					background-color: rgba(153, 153, 153, 0.3);
					border-radius: 29px;
					display: flex;
					justify-content: center;
					align-items: center;

					view {
						width: 200rpx;
						height: 40rpx;
						// background-color: #007AFF;
						display: flex;
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

		//address-nav
		.address-nav {
			width: 690rpx;
			height: 280rpx;
			display: flex;
			flex-direction: row;

			// background-color: #0077AA;
			.address-nav-item {
				width: 172rpx;
				height: 100%;
				// background-color: #FFFDEF;
				display: flex;
				flex-direction: column;
				box-sizing: border-box;
				padding: 53rpx 0 60rpx 0;
				text-align: center;

				.img {
					width: 100%;
					height: 80rpx;
					box-sizing: border-box;
					padding: 0 46rpx;
					margin-bottom: 20rpx;

					image {
						width: 100%;
						height: 100%;
					}
				}

				.text {
					padding: 0 17rpx;
					width: 100%;
					box-sizing: border-box;

					text {
						font-size: 24rpx;
						line-height: 38rpx;
						max-width: 240rpx;
						display: -webkit-box;
						-webkit-box-orient: vertical;
						-webkit-line-clamp: 2;
						overflow: hidden;
						color: #333333;
					}
				}
			}
		}

		//.detail-box
		.detail-box {
			width: 690rpx;
			// height: 600rpx;
			margin-bottom: 65rpx;
			// background-color: red;
			padding-bottom: 20rpx;
			box-shadow: 0rpx 5rpx 0rpx #EEEEEE;


			.header {
				width: 100%;
				height: 80rpx;
				// background-color: #990055;
				display: flex;
				justify-content: space-between;
				margin-bottom: 20rpx;

				.left {
					width: 596rpx;
					height: 100%;
					// background-color: #79C2EF;

					.f-row {
						width: 100%;
						height: 40rpx;
						display: flex;
						flex-direction: row;
						align-items: center;
						font-size: 32rpx;
						color: $index-font-color-one;

						image {
							width: 40rpx;
							align-items: center;
						}
					}

					.s-row {
						display: flex;
						align-items: center;
						margin-top: 11rpx;

						text {
							font-size: 22rpx;
							color: $index-font-color-two;
							line-height: 38rpx;
						}
					}

				}

				.right {
					width: 100rpx;
					height: 100%;
					display: flex;
					align-items: center;
					justify-content: center;
					font-size: 24rpx;
					color: $cloud-enjoy-nature-color;

					//立即预约
					text {
						font-weight: bold;
						line-height: 38rpx;
					}

				}
			}

			.img {
				width: 690rpx;
				height: 337rpx;
				// background-image: url(../../static/image/index/yancheng.png);
				// background-size: cover;
				box-sizing: border-box;
				padding: 20rpx 0 0 20rpx;
				position: relative;


				.back {
					width: 690rpx;
					height: 337rpx;
					position: absolute;
					top: 0;
					left: 0;
					border-radius: 6rpx;
					z-index: -1;
				}

				.img-item {
					width: 100%;
					height: 100%;
					// background-color: #0077AA;
					position: relative;
					color: #fff;

					view:nth-child(1) {
						position: absolute;
						// width: 133rpx;
						height: 50rpx;
						top: 0;
						left: 0;
						font-size: 24rpx;
						overflow: hidden;
						text-overflow: ellipsis;
						white-space: nowrap;
						max-width: 200rpx;

						// background-color: #007AFF;
						.address-icon {}
					}

					view:nth-child(2) {
						position: absolute;
						width: 253rpx;
						height: 36rpx;
						background: #1961B6;
						opacity: 0.8;
						border-radius: 18px 0px 0px 18px;

						bottom: 22rpx;
						right: 0;
						font-size: 24rpx;
						font-weight: 400;
						background-color: #007AFF;

						display: flex;
						justify-content: center;
						align-items: center;
						border-top-left-radius: 20rpx;
						border-bottom-left-radius: 20rpx;
					}
				}

				// image {
				// 	width: 100%;
				// 	height: 100%;
				// }

			}

			.body {
				width: 690rpx;
				box-sizing: border-box;
				padding: 0rpx 19rpx;

				.f-r {
					display: flex;
					justify-content: space-between;
					// margin-top: 22rpx;
					height: 52rpx;
					box-sizing: border-box;
					padding-top: 20rpx;

					.left {
						font-size: 30rpx;
						color: $index-font-color-one;
						font-weight: bold;
						width: 450rpx;
						display: flex;
						align-items: center;

						text:nth-child(1) {
							max-width: 240rpx;
							display: -webkit-box;
							-webkit-box-orient: vertical;
							-webkit-line-clamp: 1;
							overflow: hidden;
						}

						text:nth-child(2) {
							margin: 0 10rpx;
						}

						text:nth-child(3) {
							max-width: 150rpx;
							display: -webkit-box;
							-webkit-box-orient: vertical;
							-webkit-line-clamp: 1;
							overflow: hidden;
						}

					}

					.right {
						display: flex;
						width: 200rpx;
						color: $index-font-color-two;
						font-size: 22rpx;
						align-items: center;
						flex-direction: row;

						.sunui-star {
							width: 150rpx;
							height: 45rpx;
							display: flex;
							box-sizing: border-box;
							padding: 0 18rpx;
							align-items: center;
							// background-color: #0077AA;
						}
					}
				}

				.s-r {
					// line-height: 38rpx;
					// margin-top: 22rpx;
					height: 72rpx;
					box-sizing: border-box;
					padding-top: 22rpx;

					.f {
						font-size: 22rpx;
						color: $index-font-color-one;

						// text:nth-child(3) {

						// }
					}

					.s {
						width: 154rpx;
						height: 22rpx;
						margin: 0 30rpx;
						font-size: 22rpx;
						font-weight: 400;
						color: $index-font-color-one;
					}

					.t {
						width: 68rpx;
						height: 21rpx;
						font-size: 22rpx;
						font-weight: 400;
						color: $index-font-color-one;
					}
				}

				.t-r {
					// margin-top: 19rpx;
					display: flex;
					width: 680rpx;
					height: 60rpx;
					padding-top: 19rpx;

					view {
						height: 34rpx;
						box-sizing: border-box;
						padding: 6rpx 8rpx;
						border: 1px solid #666666;
						border-radius: 8rpx;
						font-size: 22rpx;
						color: $index-font-color-two;
						box-sizing: border-box;
					}

					view:nth-child(2) {
						margin-left: 33rpx;
						display: -webkit-box;
						-webkit-box-orient: vertical;
						-webkit-line-clamp: 1;
						overflow: hidden;
						max-width: 340rpx;
					}
				}
			}
		}

		//精品推荐
		.recommend {
			width: 690rpx;
			margin-top: 4rpx;
			margin-bottom: 98rpx;

			.title {
				display: flex;
				justify-content: center;
				align-items: center;
				// margin: 69rpx 0 40rpx 0;
				margin-bottom: 40rpx;

				image {
					width: 52rpx;
					height: 28rpx;
				}

				text {
					width: 253rpx;
					text-align: center;
					font-size: 32rpx;
					color: $index-font-color-one;
					font-weight: bold;
				}
			}

			.body {
				width: 690rpx;

				.f-r {
					width: 690rpx;
					height: 260rpx;
					// background-image: url(../../static/image/my/banner.png);
					// background-size: cover;
					box-sizing: border-box;
					padding: 56rpx 53rpx;
					position: relative;

					.back {
						position: absolute;
						top: 0;
						left: 0;
						width: 690rpx;
						height: 280rpx;
						z-index: -1;
						border-radius: 6rpx;
					}

					.f-r-item {
						width: 100%;
						height: 100%;
						// background-color: #007AFF;

						view:nth-child(1) {
							display: flex;
							margin-bottom: 27rpx;

							text:nth-child(1) {
								display: block;
								width: 150rpx;
								height: 38rpx;
								line-height: 38rpx;
								// background-color: #4CD964;
								font-size: 32rpx;
								color: #fff;
								font-weight: bold;
							}

							text:nth-child(2) {
								display: block;
								width: 70rpx;
								height: 38rpx;
								color: #fff;
								background-color: #1961B6;
								text-align: center;
								line-height: 38rpx;
								// background-color: #4CD964;
								font-size: 22rpx;
								border-radius: 8rpx;
							}
						}

						view:nth-child(2) {
							color: #fff;
							font-size: 22rpx;
							line-height: 34rpx;
							display: -webkit-box;
							font-weight: 400;
							-webkit-box-orient: vertical;
							-webkit-line-clamp: 3;
							overflow: hidden;
						}

					}
				}

				.s-r {
					width: 100%;
					display: flex;
					flex-wrap: wrap;
					justify-content: space-between;
					margin-top: 39rpx;

					.s-r-item {
						width: 330rpx;
						height: 540rpx;
						margin-bottom: 39rpx;
						// background-color: #0077AA;

						image {
							width: 100%;
							height: 400rpx;
							border-radius: 8rpx;
						}

						.name {
							font-weight: bold;
							line-height: 38rpx;
							color: $index-font-color-one;
							font-size: 28rpx;
							margin: 33rpx 0 0 0;
							display: -webkit-box;
							-webkit-box-orient: vertical;
							-webkit-line-clamp: 1;
							overflow: hidden;
							max-width: 300rpx;
						}

						.price {
							display: flex;
							align-items: center;
							justify-content: space-between;
							margin-top: 16rpx;
							font-weight: 400;

							view:nth-child(1) {
								font-size: 22rpx;
								color: $index-font-color-one;
								font-weight: bold;

								text {
									font-size: 40rpx;
									margin-left: -10rpx;
									// color: #1961B6;
									font-weight: bold;

								}
							}

							view:nth-child(2) {
								font-size: 22rpx;
								color: $index-font-color-two;
								font-weight: 400;

								text {
									margin: 0 10rpx 0 0;
								}
							}
						}
					}
				}
			}
		}





	}

	text {
		margin: 0;
	}

	.commin-text {
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 1;
		overflow: hidden;
		max-width: 100rpx;
	}


	//修改第三方组件样式

	/deep/ .uni-navbar--border.data-v-6bda1a90 {
		border: none !important;
	}

	/deep/.uni-searchbar.data-v-180dbe05 {
		padding: 0 !important;
		width: 580rpx !important;
		// height: 58rpx !important;
	}

	/deep/ .uni-searchbar__box.data-v-180dbe05 {
		width: 580rpx !important;
		height: 58rpx !important;
		border: none !important;
	}

	/deep/ .uni-searchbar__box-icon-search.data-v-180dbe05 {
		padding: 0 !important;
	}

	/deep/.uni-searchbar__text-placeholder.data-v-180dbe05,
	/deep/.uni-searchbar__box-search-input.data-v-180dbe05 {
		margin-left: 7rpx !important;
		font-size: 24rpx;
	}

	/deep/.uni-searchbar__cancel.data-v-180dbe05 {
		font-size: 24rpx !important;
		line-height: 48rpx !important;
	}

	/deep/.uni-navbar__header-btns-left {
		width: 300rpx !important;
	}

	/deep/ .uni-icons.data-v-a2e81f6e {
		margin-left: 5rpx;
	}

	/deep/ .data-v-57280228 .uni-searchbar__cancel.data-v-180dbe05 {
		display: flex !important;
		align-items: center !important;
		justify-content: center !important;
	}
</style>
