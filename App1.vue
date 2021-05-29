<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style lang="scss">
	/*每个页面公共css */
	@import url("./static/font/iconfont.css");

	// view {
	// 	padding-bottom: constant(safe-area-inset-bottom);  /* 兼容 iOS < 11.2 */
	// 	padding-bottom: env(safe-area-inset-bottom);  /* 兼容 iOS >= 11.2 */
	// }


	.tab-top {
		width: 750rpx;
		height: 10rpx;
		background-color: #79C2EF;
		position: fixed;
		bottom: 99rpx;
		margin-left: -30rpx;
	}

	.tabs {
		height: 118rpx;

		.tab-items {
			width: 20%;
			box-sizing: border-box;
			padding-bottom: 30rpx;
			// padding-top: 20rpx;
		}
	}

	.tab {
		// margin-top: 98rpx;
		width: 750rpx;
		height: 98rpx;
		box-sizing: content-box;
		margin-left: -30rpx;
		background-color: #79C2EF;
		position: fixed;
		bottom: 0;
		display: flex;
		flex-direction: row;
		padding-bottom: constant(safe-area-inset-bottom);
		/* 兼容 iOS < 11.2 */
		padding-bottom: env(safe-area-inset-bottom);
		/* 兼容 iOS >= 11.2 */

		/* 兼容 iOS >= 11.2 */
		.tab-item {
			width: 20%;
			height: 100%;
			// background-color: #007AFF;
			display: flex;
			justify-content: center;
			align-items: center;
			flex-direction: column;
			// text-align: center;
			color: #fff;
			font-size: 20rpx;

			image {
				width: 48rpx;
				height: 48rpx;
				margin-bottom: 5rpx;
			}
		}
	}
</style>
