<!-- 详情页 -->
<template>
	<view class="detail">
		<!-- 自定义导航 -->
		<uni-nav-bar fixed statusBar :title="title" class="status-title" @clickLeft="back">
			<uni-icons slot="left" type="arrowleft" class="status-icon"></uni-icons>
		</uni-nav-bar>
		<!-- banner -->
		<view class="banner">
			<!-- 轮播 -->
			<uni-swiper-dot :info="swiperImg" :current="current" field="content" :mode="mode" class="swiper"
				:dotsStyles="dotsStyles">
				<swiper class="swiper-box" @change="changeSwiper">
					<swiper-item v-for="(item ,index) in swiperImg" :key="index">
						<view class="swiper-item">
							<!-- <image :src="item" mode="" lazy-load></image> -->
							<image src="../../static/image/deatil/banner.png" mode=""></image>
							<view class="CornerMarker">{{current+1}}/{{ swiperImg.length }}</view>
						</view>
					</swiper-item>
				</swiper>
			</uni-swiper-dot>
		</view>
		<!-- 详情表1 -->
		<view class="detail-box">
			<!-- 第一行 -->
			<view class="detail-box-first-line">
				<view class="detail-box-first-line-left">
					<text class="price-icon">￥<text class="price">{{ detailBox.price }}</text><text
							class="price-company">元</text></text>
				</view>
				<view class="detail-box-first-line-right">
					<text>月销
						<text
							class="number">{{ detailBox.num>=10000? Math.floor( detailBox.num/10000)+'w' : detailBox.num}}+</text>
					</text>
				</view>
			</view>
			<!-- 第二行 -->
			<view class="detail-box-second-line">
				<view class="detail-box-second-line-left">
					<text class="name go-beyond-no-flex">{{detailBox.name}}</text>
				</view>
				<view class="detail-box-second-line-right">
					<image src="../../static/image/deatil/share.png" mode="heightFix"></image>
				</view>
			</view>
			<!-- 第三行 -->
			<view class="detail-box-third-line">
				<text class="pin" v-for="item in detailBox.keyword">{{ item.text }}</text>
			</view>
		</view>
		<!-- 规格 -->
		<view class="Specifications">
			<!-- 第一行 -->
			<view class="Specifications-first-line">
				<view class="Specifications-first-line-first-column">
					<text>选择</text>
				</view>
				<view class="Specifications-first-line-second-column">
					<text>已选：{{ Specifications.Specification }}</text>
				</view>
				<view class="Specifications-first-line-third-column">
					<image src="../../static/image/my/READMORE.png" mode=""></image>
				</view>
			</view>
			<!-- 第二行 -->
			<view class="Specifications-second-line">
				<view class="Specifications-second-line-first-column">
					<text>运费</text>
				</view>
				<view class="Specifications-second-line-second-column">
					<text>在线支付运费(以实际支付为准)</text>
				</view>
			</view>
		</view>
		<!-- 评价 -->
		<view class="evaluate">
			<!-- 第一行 -->
			<view class="evaluate-first-line" v-if="isEvaluate">
				<!-- 第一行 左-->
				<view class="evaluate-first-line-left">
					<text class="evaluate-first-line-left-title">商品评价(3)</text>
				</view>
				<!-- 第一行 右-->
				<view class="evaluate-first-line-right">
					<view class="evaluate-first-line-right-more" @click="more"><text class="">查看更多</text>
						<image src="../../static/image/my/READMORE.png" mode=""></image>
					</view>
				</view>
			</view>
			<!-- 第二行 -->
			<view class="evaluate-second-line" v-for="(item,index) in evaluate" :key="index">
				<!-- 第二行 第一行-->
				<view class="evaluate-second-line-first">
					<!-- 第二行 第一行 左-->
					<view class="evaluate-second-line-first-left">
						<image :src="item.headPortrait" mode=""></image>
					</view>
					<!-- 第二行 第一行 右-->
					<view class="evaluate-second-line-first-right">
						<!-- 昵称 -->
						<view class="evaluate-second-line-first-right-nick">
							<text>{{ item.nick }}</text>
						</view>
						<!-- 时间 -->
						<view class="evaluate-second-line-first-right-time">
							<text>5天前</text>
						</view>
					</view>
				</view>
				<!-- 第二行 第二行-->
				<view class="evaluate-second-line-second">
					<text>{{item.evaluate}}</text>
				</view>
			</view>
		</view>
		<!-- 宝贝详情 -->
		<view class="BabyDetails">
			<!-- 标题 -->
			<view class="BabyDetails-title">
				<view class="BabyDetails-title-left"></view>
				<view class="BabyDetails-title-center">
					<text>宝贝详情</text>
				</view>
				<view class="BabyDetails-title-right"></view>
			</view>
			<view class="BabyDetails-body">
				<image :src="detailImg" mode="widthFix"></image>
			</view>
		</view>


	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '商品详情',
				none: true,
				current: 0,
				mode: 'none',
				swiperCurrent: 0,
				swiperImg: [
					'../../static/image/index/banner6.png',
					'../../static/image/index/banner6.png'
				],
				detailBox: {
					price: 98.8,
					num: 100000,
					name: '青海特产风干牦牛肉干青海精品超干手撕 牦牛肉干500g正宗麻辣零食',
					keyword: [{
							text: '回味悠长'
						},
						{
							text: '扑鼻浓香'
						},
						{
							text: '肉香浓郁'
						},
						{
							text: '顺丰包邮'
						}
					]
				},
				Specifications: {
					Specification: '五香味500g【收藏加购送奶片】'
				},
				isEvaluate: true,
				evaluate: [{
						nick: '云享小王子',
						headPortrait: '../../static/image/deatil/headPortrait.png',
						evaluate: '麻辣味道挺好的，已经推荐给朋友，很好吃',
					},
					{
						nick: '云享小王子',
						headPortrait: '../../static/image/deatil/headPortrait.png',
						evaluate: '麻辣味道挺好的，已经推荐给朋友，很好吃'
					}

				],
				detailImg: '../../static/image/deatil/detail_image.png'
			};
		},
		methods: {
			changeSwiper(e) {
				console.log(e.detail);
				this.current = e.detail.current;
			},
			back() {
				uni.navigateBack({
					delta: 1
				})
			},
			more() {
				uni.navigateTo({
					url: '../evaluate/evaluate'
				})
			}
		}
	}
</script>

<style lang="scss">
	.detail {
		padding: 0 30rpx;
		.status-title {
			font-size: 34rpx;
			font-family: PingFang;
			font-weight: bold;
			color: #000000;

			.status-icon {
				font-size: 30rpx;
			}
		}

		//banner
		.banner {
			width: 690rpx;
			height: 750rpx;

			// margin-top: 15rpx;
			swiper {
				height: 750rpx;
			}

			.swiper {
				width: 690rpx;
				height: 750rpx;
				border-radius: 16rpx;
				overflow: hidden;

				.swiper-item {
					width: 690rpx;
					height: 750rpx;

					image {
						width: 690rpx;
						height: 750rpx;
						display: block;
						box-sizing: border-box;
						border-radius: 6rpx;

					}

					.CornerMarker {
						width: 70rpx;
						height: 30rpx;
						position: absolute;
						right: 30rpx;
						bottom: 30rpx;
						background: #000000;
						opacity: 0.5;
						border-radius: 15rpx;
						font-size: 20rpx;
						font-family: PingFang;
						font-weight: 400;
						color: #FFFFFF;
						display: flex;
						justify-content: center;
						align-items: center;
					}

				}
			}
		}

		// 详情
		.detail-box {
			width: 690rpx;
			height: 250rpx;
			background-color: #fff;
			box-sizing: border-box;
			padding: 25rpx 19rpx 31rpx 19rpx;
			margin-top: 26rpx;
			box-shadow: 0 10rpx 19rpx 3rpx rgba(153, 153, 153, 0.08);

			.detail-box-first-line {
				width: 100%;
				height: 43rpx;
				// background-color: red;
				display: flex;
				justify-content: space-between;

				.detail-box-first-line-left {
					width: 544rpx;
					height: 100%;
					// background-color: #4CD964;

					.price-icon {
						font-size: 22rpx;
						font-family: PingFang;
						font-weight: bold;
						// color: #FA3117;
						line-height: 38rpx;

						.price {
							font-size: 60rpx;
							font-family: DINCond;
							font-weight: bold;
							color: #FA3117;
							line-height: 38rpx;

							.price-company {
								font-size: 22rpx;
								font-family: PingFang;
								font-weight: 400;
								color: #333333;
								line-height: 38rpx;
							}
						}
					}

				}

				.detail-box-first-line-right {
					width: 127rpx;
					height: 100%;
					display: flex;

					// justify-content: center;
					// align-items: center;
					text:nth-child(1) {
						font-size: 22rpx;
						font-family: PingFang;
						font-weight: 400;
						color: #333333;
						line-height: 38rpx;

						.number {}
					}
				}
			}

			.detail-box-second-line {
				width: 690rpx;
				height: 74rpx;
				// background-color: #795DA3;
				margin-top: 27rpx;
				margin-bottom: 27rpx;
				position: relative;

				.detail-box-second-line-left {
					width: 538rpx;
					height: 100%;
					// background-color: #9A6E3A;

					.name {
						font-size: 30rpx;
						font-family: PingFang;
						font-weight: bold;
						color: #333333;
						line-height: 46rpx;
					}
				}

				.detail-box-second-line-right {
					width: 44rpx;
					height: 100%;
					position: absolute;
					right: 19rpx;
					top: 0;

					// background-color: #A71D5D;
					image {
						width: 40rpx;
						height: 40rpx;
					}
				}
			}

			.detail-box-third-line {
				width: 435rpx;
				height: 22rpx;
				// background-color: #9A6E3A;
				display: flex;
				align-items: center;

				.pin {
					font-size: 22rpx;
					font-family: PingFang;
					font-weight: 400;
					color: #666666;
					display: flex;
					align-items: center;
					line-height: 38rpx;
					margin-right: 10rpx;
				}
			}
		}

		// 规格
		.Specifications {
			width: 690rpx;
			height: 150rpx;
			// background-color: #795DA3;
			box-sizing: border-box;
			padding: 37rpx 19rpx 38rpx 19rpx;
			background: #FDFDFD;
			box-shadow: 0px 10px 19px 3px rgba(153, 153, 153, 0.08);
			border-radius: 8px;

			.Specifications-first-line {
				width: 100%;
				height: 25rpx;
				// background-color: #669900;
				display: flex;
				position: relative;

				.Specifications-first-line-first-column {
					width: 60rpx;
					height: 100%;
					// background-color: #79C2EF;
					display: flex;
					align-items: center;

					text {
						font-size: 26rpx;
						font-family: PingFang;
						font-weight: bold;
						color: #333333;
						line-height: 38rpx;
					}
				}

				.Specifications-first-line-second-column {
					width: 420rpx;
					height: 100%;
					// background-color: #666666;
					display: flex;
					margin-left: 36rpx;
					max-width: 420rpx;
					align-items: center;

					text {
						font-size: 24rpx;
						font-family: PingFang;
						font-weight: 400;
						color: #333333;
						line-height: 38rpx;
						overflow: hidden;
						text-overflow: ellipsis;
						white-space: nowrap;
					}
				}

				.Specifications-first-line-third-column {
					width: 20rpx;
					height: 100%;
					// background-color: #990055;
					position: absolute;
					right: 0;
					top: 0;

					image {
						width: 20rpx;
						height: 20rpx;
						position: absolute;
						right: 0;
						top: 0;
					}
				}
			}

			.Specifications-second-line {
				width: 100%;
				height: 25rpx;
				// background-color: #669900;
				display: flex;
				position: relative;
				margin-top: 26rpx;

				.Specifications-second-line-first-column {
					width: 60rpx;
					height: 100%;
					// background-color: #79C2EF;
					display: flex;
					align-items: center;

					text {
						font-size: 26rpx;
						font-family: PingFang;
						font-weight: bold;
						color: #333333;
						line-height: 38rpx;
					}
				}

				.Specifications-second-line-second-column {
					width: 420rpx;
					height: 100%;
					// background-color: #666666;
					display: flex;
					margin-left: 36rpx;
					max-width: 420rpx;
					align-items: center;

					text {
						font-size: 24rpx;
						font-family: PingFang;
						font-weight: 400;
						color: #333333;
						line-height: 38rpx;
					}
				}
			}
		}

		/* 评价 */
		.evaluate {
			width: 690rpx;
			height: 467rpx;
			box-sizing: border-box;
			padding: 35rpx 19rpx 34rpx 20rpx;
			background: #FDFDFD;
			box-shadow: 0px 10px 19px 3px rgba(153, 153, 153, 0.08);
			border-radius: 8px;

			// background-color: #0077AA;
			.evaluate-first-line {
				width: 100%;
				height: 29rpx;
				// background-color: #55A532;
				display: flex;
				justify-content: space-between;

				.evaluate-first-line-left {
					width: 547rpx;
					height: 100%;
					// background-color: #990055;
					display: flex;
					align-items: center;

					.evaluate-first-line-left-title {
						font-size: 30rpx;
						font-family: PingFang;
						font-weight: bold;
						color: #333333;
						line-height: 38rpx;
					}
				}

				.evaluate-first-line-right {
					width: 143rpx;
					height: 100%;
					// background-color: #666666;
					display: flex;
					justify-content: center;
					align-items: center;

					.evaluate-first-line-right-more {
						display: flex;
						justify-content: flex-end;
						align-items: center;

						text {
							font-size: 24rpx;
							font-family: PingFang;
							font-weight: 400;
							color: #999999;
							line-height: 38rpx;
						}

						image {
							width: 20rpx;
							height: 20rpx;
							margin-left: 19rpx;
						}

					}
				}

			}

			.evaluate-second-line {
				width: 100%;
				// height: 300rpx;
				// background-color: #1961B6;
				margin-top: 44rpx;

				.evaluate-second-line-first {
					width: 100%;
					height: 70rpx;
					// background-color: #795DA3;
					display: flex;
					flex-direction: row;

					.evaluate-second-line-first-left {
						width: 70rpx;
						height: 70rpx;

						image {
							width: 70rpx;
							height: 70rpx;
						}
					}

					.evaluate-second-line-first-right {
						width: 620rpx;
						height: 100%;
						margin-left: 23rpx;
						// background-color: #9A6E3A;
						display: flex;
						flex-direction: column;

						.evaluate-second-line-first-right-nick {
							display: flex;
							align-items: center;

							text {
								font-size: 24rpx;
								font-family: PingFang;
								font-weight: bold;
								color: #333333;
								line-height: 38rpx;
							}
						}

						.evaluate-second-line-first-right-time {
							display: flex;
							align-items: center;

							text {
								font-size: 22rpx;
								font-family: PingFang;
								font-weight: 400;
								color: #999999;
								line-height: 38rpx;
							}
						}
					}
				}

				.evaluate-second-line-second {
					text {
						font-size: 24rpx;
						font-family: PingFang;
						font-weight: 400;
						color: #333333;
						line-height: 38rpx;
					}
				}
			}
		}

		/* 宝贝详情 */
		.BabyDetails {
			width: 690rpx;
			height: 680rpx;
			// background-color: #F0AD4E;
			margin-top: 64rpx;
			margin-bottom: 30rpx;
			box-sizing: border-box;
			padding-bottom: constant(safe-area-inset-bottom); //兼容 IOS<11.2
			padding-bottom: env(safe-area-inset-bottom); //兼容 IOS>11.2

			.BabyDetails-title {
				box-sizing: border-box;
				padding: 0 84rpx;
				width: 100%;
				height: 28rpx;
				// background-color: #DF5000;
				display: flex;
				align-items: center;
				justify-content: space-between;

				.BabyDetails-title-left {
					width: 180rpx;
					height: 1px;
					background: #999999;

				}

				.BabyDetails-title-center {
					text {
						font-size: 30rpx;
						font-family: PingFang;
						font-weight: bold;
						color: #333333;
						line-height: 38rpx;
					}
				}

				.BabyDetails-title-right {
					width: 180rpx;
					height: 1px;
					background: #999999;
				}
			}

			.BabyDetails-body {
				margin-top: 35rpx;

				image {
					width: 100%;
				}
			}
		}

		//goods
		.goods {
			width: 690rpx;
			position: fixed;
			bottom: 0;
			// background-color: #FFECEC;
			box-sizing: content-box;
			padding-bottom: constant(safe-area-inset-bottom); //兼容 IOS<11.2
			padding-bottom: env(safe-area-inset-bottom); //兼容 IOS>11.2
		}

		//修改第三方组件样式
		/deep/ .uni-navbar--border.data-v-6bda1a90 {
			border: none !important;
		}
	}
</style>
