<template>
	<view class="shopType">
		<uni-nav-bar fixed="true" class="status_title" color="#000000" statusBar="true" :title="title"
			@clickLeft="back">
			<uni-icons slot="left" type="arrowleft" class="status-icon" size="17"></uni-icons>
		</uni-nav-bar>
		<view class="shopType-nav">
			<view class="shopType-nav-item" v-for="(item,index) in shopTypeNav" :key="index"
				:class="active==index?'active':''" :style="{color:active==index?'#FECE0A':'#333333'}"
				@click="shopTypeNavClick(index)">
				<view class="left">
					<text>{{ item.text }}</text>
				</view>
				<view class="right">
					<text :class="item.sortIcon?'iconfont icon-paixushang':''"></text>
					<text :class="item.sortIcon?'iconfont icon-paixuxia':''"></text>
				</view>
			</view>
		</view>
		<view class="shopType-body" v-for="(item,index) in shopTypeBody" :key="index">
			<view class="shopType-body-item">
				<view class="shopType-body-item-left">
					<image :src="item.img" mode=""></image>
				</view>
				<view class="shopType-body-item-right">
					<view class="shopType-body-item-right-first-line">
						<text class="oh2">{{ item.name }}</text>
					</view>
					<view class="shopType-body-item-right-second-line">
						<view class="item" v-for="tag in item.tags">
							<text class="oh1">{{ tag.text }}</text>
						</view>
					</view>
					<view class="shopType-body-item-right-third-line">
						<view class="left">
							<text>￥<text>{{item.price}}</text><text>元</text></text>
						</view>
						<view class="right">
							<text>已售<text>{{item.num>10000?parseInt(item.num/10000)+'w+':item.num}}</text></text>
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: "",
				active: 0,
				shopTypeNav: [{
						text: '默认排序',
						sortIcon: false
					},
					{
						text: '销量排序',
						sortIcon: true
					},
					{
						text: '价格排序',
						sortIcon: true
					}
				],
				shopTypeBody: [{
						img: '../../static/image/shopType/banner.png',
						name: '青海特产风干藏牦牛肉精品肉干超干手撕牦牛肉干500g正宗麻辣',
						price: 300,
						num: 20000,
						tags: [{
								text: '新品包邮'
							},
							{
								text: '公益'
							}
						]
					},
					{
						img: '../../static/image/shopType/banner.png',
						name: '青海特产风干藏牦牛肉精品肉干超干手撕牦牛肉干500g正宗麻辣',
						price: 300,
						num: 20000,
						tags: [{
								text: '新品包邮'
							},
							{
								text: '公益'
							}
						]
					}


				]
			};
		},
		onLoad(e) {
			this.title = e.text;
		},
		methods: {
			back() {
				uni.navigateBack({
					delta: 1
				})
			},
			shopTypeNavClick(index) {
				this.active = index;
				console.log(this.active)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.shopType {
		box-sizing: border-box;
		padding: 0 30rpx;

		.status_title {
			font-size: 34rpx;
			font-family: PingFang;
			font-weight: bold;
		}

		.shopType-nav {
			width: 690rpx;
			height: 29rpx;
			display: flex;
			margin-top: 36rpx;
			justify-content: space-between;

			.shopType-nav-item {
				width: 33.3%;
				height: 100%;
				display: flex;
				align-items: center;
				justify-content: center;
				font-size: 28rpx;
				font-family: PingFang;
				font-weight: bold;

				.right {
					display: flex;
					flex-direction: column;
					align-items: center;
					margin-left: 15rpx;
				}
			}
		}

		.shopType-body {
			width: 690rpx;
			height: 256rpx;
			margin-top: 45rpx;
			box-sizing: border-box;
			padding: 29rpx 25rpx 27rpx 19rpx;
			background: #FFFFFF;
			box-shadow: 0px 10rpx 19rpx 3rpx rgba(153, 153, 153, 0.08);
			border-radius: 8rpx;
			margin-bottom:26rpx;

			.shopType-body-item {
				width: 100%;
				height: 100%;
				// background-color: #DD524D;
				display: flex;

				.shopType-body-item-left {
					width: 200rpx;
					height: 100%;

					image {
						width: 100%;
						height: 100%;
					}
				}

				.shopType-body-item-right {
					width: 471rpx;
					height: 100%;
					// background-color: #666666;
					box-sizing: border-box;
					padding-left: 28rpx;
					padding-top: 7rpx;

					.shopType-body-item-right-first-line {
						width: 418rpx;
						height: 70rpx;
						// background-color: #79C2EF;
						font-size: 28rpx;
						font-family: PingFang;
						font-weight: bold;
						color: #333333;
						line-height: 44rpx;
						display: flex;
						align-items: center;
					}

					.shopType-body-item-right-second-line {
						width: 418rpx;
						height: 34rpx;
						margin-top: 18rpx;
						display: flex;

						.item {
							max-width: 126rpx;
							height: 100%;
							border: 1px solid #666666;
							border-radius: 8px;
							font-size: 22rpx;
							font-family: PingFang;
							font-weight: 400;
							color: #666666;
							line-height: 38rpx;
							display: flex;
							align-items: center;
							justify-content: center;
							margin-right: 21rpx;
							box-sizing: border-box;
							padding: 6rpx 17rpx;
						}
					}

					.shopType-body-item-right-third-line {
						width: 418rpx;
						height: 29rpx;
						margin-top: 33rpx;
						display: flex;
						justify-content: space-between;

						.left {
							display: flex;
							align-items: center;
							justify-content: flex-start;
							font-size: 22rpx;
							font-family: PingFang;
							font-weight: bold;
							color: #FA3117;
							line-height: 38rpx;

							text {
								text:nth-child(1) {
									font-size: 40rpx;
									font-family: DINCond;
									font-weight: bold;
									line-height: 38rpx;
									margin-left: 7rpx;
								}

								text:nth-child(2) {
									font-family: PingFang;
									font-weight: 400;
									color: #333333;
									margin-left: 10rpx;
								}
							}
						}

						.right {
							font-size: 22rpx;
							font-family: PingFang;
							font-weight: 400;
							color: #999999;
							line-height: 38rpx;
							display: flex;
							align-items: center;
							justify-content: flex-end;

							text {
								text:nth-child(1) {
									margin-left: 10rpx;
								}
							}
						}
					}
				}
			}
		}
	}

	.active {
		color: #FECE0A;
	}

	.icon-paixushang,
	.icon-paixuxia {
		font-size: 17rpx;
		color: #999999;
	}

	//修改第三方组件样式

	/deep/ .uni-navbar--border.data-v-6bda1a90 {
		border: none !important;
	}
</style>
