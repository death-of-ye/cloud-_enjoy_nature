<template>
	<view class="address-nav">
		<view class="address-nav-item" v-for="(item,index) in addressNav" :key="index" @click="address_nav_to(item)">
			<view class="img">
				<image :src="item.img" mode="widthFix"></image>
			</view>
			<view class="text">
				<text>{{ item.text }}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: "address-nav",
		props:[
			'addressNav'
		],
		data() {
			return {

			};
		}
	}
</script>

<style lang="scss">
	.address-nav {
		width: 690rpx;
		height: 139rpx;
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
			padding: 59rpx 0 0rpx 0;
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
</style>
