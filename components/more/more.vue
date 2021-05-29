<template>
	<view class="more">
		<view class="left">
			<image :src="leftImg" mode=""></image>
			{{text}}
		</view>
		<view class="right">
			<image :src="rightImg" mode=""></image>
		</view>
	</view>
</template>

<script>
	export default {
		name: "more",
		props:{
			'leftImg',
			'rightImg',
			'text'
		}
		data() {
			return {

			};
		}
	}
</script>

<style lang="scss">
	.more {
		width: 690rpx;
		display: flex;
		justify-content: space-between;

		.left {
			width: 649rpx;
			display: flex;
			align-items: center;
			margin-left: 30rpx;

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
</style>
