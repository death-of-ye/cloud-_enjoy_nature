<template>
	<view class="evaluateView">
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
						<text>5天前&nbsp;</text>
						<text v-if="!isEvaluate">|nbsp;</text>
					</view>
				</view>
			</view>
			<!-- 第二行 第二行-->
			<view class="evaluate-second-line-second">
				<text>{{item.evaluate}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "evaluate",
		props: [
			'evaluate'
		],
		data() {
			return {
				isEvaluate: false
			};
		}
	}
</script>

<style lang="scss">
	.evaluateView {
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
</style>
