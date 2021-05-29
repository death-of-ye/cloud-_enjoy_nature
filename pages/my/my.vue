<template>
	<view class="my">
		<view v-if="isRow" :class="isRow?'box box1':'box'" :style="{opacity:opacity}">
			<view class="title">我的</view>
		</view>
		<view class="header">

			<!--  -->

			<view class="logo" :style="{marginTop:isTop?168+'rpx':148+'rpx',marginBottom:isTop?121+'rpx':141+'rpx'}">
				<view class="left">
					<image :src="headPortrait" mode="" lazy-load></image>
					<text class="nick" style="">{{Nickname}}</text>
				</view>
				<view class="right">
					<view class="">修改资料</view>
				</view>

			</view>
		</view>
		<view class="my_nav">
			<view class="">
				<view class="" v-for="(item,index) in my_nav" :key="index" @click="my_nav_to(item.url)">
					<image :src="item.img" mode="heightFix" lazy-load></image>
					<text>{{ item.text }}</text>
				</view>
			</view>
		</view>
		<view class="my_order">
			<view class="f-r">
				<view class="left">我的订单</view>
				<view class="right">查看全部<image src="../../static/image/my/READMORE.png" mode="heightFix"
						style="height: 20rpx;"></image>
				</view>
			</view>
			<view class="s-r">
				<view class="" v-for="(item,index) in my_order" :key="index" @click="my_order_to(item.url)">
					<image :src="item.img" mode="aspectFit" lazy-load></image>
					<text>{{ item.text }}</text>
				</view>
			</view>
		</view>
		<view class="more" v-for="(item,index) in more" :key="index" @click="more_to(item.url)">
			<view class="left">
				<image :src="item.img" mode=""></image>
				{{ item.text }}
			</view>
			<view class="right">
				<image src="../../static/image/my/READMORE.png" mode="" lazy-load></image>
			</view>
		</view>
		<view class="" style="width: 750rpx;height: 98rpx;"></view>
		
		<!-- tab -->
		<view class="tab">
			<view class="tab-item" v-for="(item,index) in tab" :key="index" @click="navTo(item.url)">
				<image :src="item.img" mode="heightFix" lazy-load></image>
				<text>{{item.text}}</text>
			</view>
		</view>
		<!-- <more :leftImg="kefu.leftImg" :rightImg="kefu.rightImg" :text="kefu.title"></more> -->
	</view>
</template>

<script>
	import rate from '../../components/rate/rate.vue'
	export default {
		components: {
			rate
		},
		data() {
			return {
				isTop: false,
				isRow: false,
				opacity: 0,
				headPortrait: '../../static/image/my/headPortrait.png',
				Nickname: '超爱喝饮料',
				kefu: {
					leftImg: "../../static/image/icon/desert-svgrepo-com1@2x.png",
					rightImg: "../../static/image/icon/desert-svgrepo-com1@2x.png",
					"title": "联系客服"
				},
				my_nav: [{
						img: '../../static/image/my/Personalcollection.png',
						text: '个人收藏',
						url: 'url1'
					},
					{
						img: '../../static/image/my/makeAnappointment.png',
						text: '我的预约',
						url: 'url2'
					},
					{
						img: '../../static/image/my/Finance.png',
						text: '财务记录',
						url: 'url3'
					},
					{
						img: '../../static/image/my/address.png',
						text: '收货地址',
						url: 'url4'
					}

				],
				my_order: [{
						img: '../../static/image/my/payment.png',
						text: '代付款',
						url: 'url1'
					},
					{
						img: '../../static/image/my/ToBeDelivered.png',
						text: '代发货',
						url: 'url2'
					},
					{
						img: '../../static/image/my/ToBePickedUp.png',
						text: '待收货',
						url: 'url3'
					},
					{
						img: '../../static/image/my/Completed.png',
						text: '已完成',
						url: 'url4'
					},
					{
						img: '../../static/image/my/ReturnAndExchange.png',
						text: '退换货',
						url: 'url5'
					},

				],
				more: [{
						img: '../../static/image/my/ke.png',
						text: '联系客服',
						url: ''
					},
					{
						img: '../../static/image/my/AboutMy.png',
						text: '关于我们',
						url: ''
					},
					{
						img: '../../static/image/my/PrivacyPolicy.png',
						text: '隐私政策',
						url: ''
					},
					{
						img: '../../static/image/my/UserAgreement.png',
						text: '用户协议',
						url: ''
					}
				],
				tab: [{
						img: '../../static/image/my/cao@2x.png',
						text: '首页',
						url: '/pages/index/index'
					},
					{
						img: '../../static/image/my/yuanwei@2x.png',
						text: '环境教育',
						url: '/pages/index/index'
					},
					{
						img: '../../static/image/my/zhiwu@2x.png',
						text: '商城',
						url: '/pages/index/index'
					},
					{
						img: '../../static/image/my/shucai-@2x.png',
						text: '购物车',
						url: '/pages/index/index'
					},
					{
						img: '../../static/image/my/cao2@2x.png',
						text: '我的',
						url: '/pages/index/index'
					},

				]
			};
		},
		//监测滚动
		onPageScroll(e) {
			if (e.scrollTop >= 40) {
				console.log(e.scrollTop)
				let timer = setInterval(() => {
					this.opacity += 0.1
					if ((this.opacity > 0.7 && this.opacity < 1) || this.opacity > 1) {
						clearTimeout(timer);
						this.isRow = true;
					}
				}, 1000)

			}
			if (e.scrollTop == 0) {
				console.log(e.scrollTop)
				this.opacity = 1;
				let timers = setInterval(() => {
					// console.log(this.opacity + ',1')
					if (this.opacity >= 2) {
						this.opacity -= 1;
					}
					// console.log(this.opacity + ',2')
					this.opacity -= 0.1;
					if (this.opacity <= 0) {
						clearTimeout(timers);
						this.isRow = false;
					}
				}, 1000)
			}
		},
		onShow() {
			// plus.navigator.setFullscreen(true)
		},
		onReady() {
			uni.getSystemInfo({
				success: e => {
					// console.log(e)
					if (e.model == 'iPhone X' || e.model == 'iPhone XR' || e.model ==
						'iPhone XS Max' || e.windowWidth < 375) {
						this.isTop = true;
					} else {
						this.isTop = false;
					}
				}
			})
		},
		methods: {
			formatDecimal(num, decimal) {
				num = num.toString()
				let index = num.indexOf('.')
				if (index !== -1) {
					num = num.substring(0, decimal + index + 1)
				} else {
					num = num.substring(0)
				}
				return parseFloat(num).toFixed(decimal)
			},
			//tab跳转
			navTo(url) {
				// console.log(url);
				uni.redirectTo({
					url: url
				});
			},
			//更多跳转
			more_to(url) {
				console.log(url);
				uni.redirectTo({
					url: url
				});
			},
			//导航跳转
			my_nav_to(url) {
				console.log(url);
				uni.redirectTo({
					url: url
				});
			},
			//订单跳转
			my_order_to(url) {
				console.log(url);
				uni.redirectTo({
					url: url
				});
			}


		}
	}
</script>

<style lang="scss">
	page {
		padding: 0;

	}

	// text{
	// 	font-weight: bold;
	// }

	.my {

		.box {
			width: 750rpx;
			height: 128rpx;
			// background-color: #;

		}

		.box1 {
			position: fixed;
			z-index: 998;
			transition: width 2s, height 2s, transform 2s;
			background: #fff;
			transition: opacity 2s ease;
			left: 0;
			right: 0;

			.title {
				width: 750rpx;
				height: 65rpx;
				// background-color: #0077AA;
				color: #eb4c50;
				font-weight: bold;
				position: relative;
				top: 57rpx;
				box-sizing: border-box;
				padding-left: 30rpx;
				display: flex;
				align-items: center;

			}
		}

		.header {
			width: 750rpx;
			height: 409rpx;
			display: flex;
			background-image: url(../../static/image/my/backgroundTitle.png);
			background-position: -1, 0;
			background-size: cover;
			// align-items: center;
			// padding-top: 60rpx;
			// position: relative;



			.logo {
				width: 750rpx;
				height: 120rpx;
				// background-color: #0077AA;
				display: flex;
				box-sizing: border-box;
				align-items: center;
				box-sizing: border-box;
				padding: 0 30rpx;
				// // margin: 148rpx 0 141rpx 0;
				// margin-top: 148rpx;
				// margin-bottom: 141rpx;

				// position: absolute;
				// top: constant(safe-area-inset-bottom);
				// /* 兼容 iOS < 11.2 */
				// top: env(safe-area-inset-bottom);
				/* 兼容 iOS >= 11.2 */

				// padding: 232rpx 30rpx 282rpx 30rpx;
				// margin: 32rpx 0 282rpx 0;
				// padding: 0 30rpx;
				// position: relative;
				// top: 0;
				// left: 0;

				.left {
					width: 590rpx;
					height: 120rpx;
					// background-color: #DF5000;
					display: flex;
					align-items: center;
					font-size: 27rpx;

					.nick {
						margin-left: 37rpx;
						color: #fff;
						font-size: 37rpx;
						overflow: hidden;
						text-overflow: ellipsis;
						white-space: nowrap;
						max-width: 200rpx;
					}

					image {
						width: 120rpx;
						height: 120rpx;
					}
				}

				.right {
					width: 160rpx;
					height: 60rpx;
					// background-color: #669900;
					display: flex;
					align-items: center;
					font-size: 24rpx;
					box-sizing: border-box;
					padding-top: 0;
					font-weight: bold;
					view {
						display: flex;
						justify-content: center;
						align-items: center;
						width: 100%;
						height: 60rpx;
						background-color: #fff;
						border-radius: 30rpx;
						color: #EB4C50;
						box-shadow: 0px 10px 19px 3px rgba(194, 0, 5, 0.15);
					}
				}

			}
		}




		.my_nav {
			width: 750rpx;
			height: 130rpx;
			display: flex;
			// flex-direction: column;
			justify-content: center;

			// margin-left:202rpx;
			view {
				width: 690rpx;
				height: 180rpx;
				margin-top: -90rpx;
				background-color: #fff;
				box-shadow: 0rpx 5rpx 0rpx #EEEEEE;
				display: flex;
				z-index: 99;

				view {
					width: 25%;
					height: 180rpx;
					margin-top: 0;
					// background-color: #0077AA;
					box-sizing: border-box;
					// padding: 38rpx;
					display: flex;
					justify-content: center;
					flex-direction: column;
					align-items: center;

					image {
						width: 51rpx;
						height: 51rpx;
						margin-bottom: 26rpx;
					}

					text {
						font-size: 26rpx;
						font-weight: 400;
						line-height: 38rpx;
					}
				}
			}

		}

		.my_order {
			width: 750rpx;
			// background-color: #DD4A68;
			padding: 0 30rpx;
			margin-bottom: 85rpx;
			margin-top: -11rpx;

			.f-r {
				width: 690rpx;
				height: 80rpx;
				box-sizing: border-box;
				padding: 47rpx 0;
				// background-color: #F0AD4E;
				display: flex;
				justify-content: space-between;
				align-items: center;
				font-size: 32rpx;

				.left {
					font-weight: bold;
					font-size: 32rpx;
				}

				.right {
					font-size: 24rpx;
					display: flex;
					align-items: center;
					font-weight: 400;
					color: #666666;
					line-height: 38rpx;

					text {
						margin-right: 18rpx;
					}
				}
			}

			.s-r {
				width: 690rpx;
				height: 102rpx;
				// background-color: #0077AA;
				display: flex;
				flex-direction: row;

				view {
					width: 20%;
					display: flex;
					flex-direction: column;
					justify-content: center;
					align-items: center;
					font-size: 26rpx;

					image {
						width: 52rpx;
						height: 49rpx;
						margin-bottom: 26rpx;
					}

					text {
						font-size: 26rpx;
						font-family: PingFang;
						font-weight: 400;
						color: #333333;
						line-height: 38rpx;
					}
				}

			}
		}

		.more {
			width: 690rpx;
			display: flex;
			justify-content: space-between;
			margin-bottom: 57rpx;

			.left {
				width: 649rpx;
				display: flex;
				align-items: center;
				margin-left: 30rpx;
				font-size: 26rpx;
				font-weight: 400;
				color: #333333;

				image {
					width: 40rpx;
					height: 40rpx;
					margin-right: 21rpx;
				}
			}

			.right {
				width: 30rpx;
				display: flex;
				align-items: center;

				image {
					width: 30rpx;
					height: 30rpx;
				}
			}
		}

		.tab {
			margin-left: 0;
		}

		// .tab {
		// 	// margin-top: 98rpx;
		// 	width: 750rpx;
		// 	height: 98rpx;
		// 	box-sizing: border-box;
		// 	// margin-left: -30rpx;
		// 	background-color: #eb4c50;
		// 	position: fixed;
		// 	margin-top: 100rpx;
		// 	bottom: 0;
		// 	display: flex;
		// 	flex-direction: row;


		// 	.tab-item {
		// 		width: 20%;
		// 		height: 100%;
		// 		// background-color: #007AFF;
		// 		display: flex;
		// 		justify-content: center;
		// 		align-items: center;
		// 		flex-direction: column;
		// 		// text-align: center;
		// 		color: #fff;
		// 		font-size: 20rpx;

		// 		image {
		// 			width: 48rpx;
		// 			height: 48rpx;
		// 			margin-bottom: 5rpx;
		// 		}
		// 	}
		// }
	}
</style>
