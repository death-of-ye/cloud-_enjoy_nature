<script>
	import Vue from 'vue'
	import {
		mapState,
		mapMutations
	} from 'vuex'
	export default {
		onLaunch: function() {
			console.log('App Launch');
			// let uniIdToken = uni.getStorageSync('token')
			// console.log(uniIdToken,'app')
			// if (uniIdToken) {
			// 	api.wxlogin()
			// 	// this.login(uni.getStorageSync('userinfo'))
			// }
			let username = uni.getStorageSync('userinfo') // 判断有没有openid，有则说明登录过了，重新把缓存存进vuex
			if (username) {
				uni.getStorage({
					key: 'userinfo',
					success: (res) => {
						this.login(res.data)
					}
				})
			}
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		},
		methods: {
			...mapMutations(['login']),
		},
	}
</script>
<style lang="scss">
	/*每个页面公共css */
	// @import "uview-ui/index.scss";
	// @import 'styles/base.scss';
	@import url("./static/font/iconfont.css");

	//不要修改
	.status-bar {
		height: var(--status-bar-height);
		width: 100%;
	}

	uni-checkbox .uni-checkbox-input.uni-checkbox-input-checked:before {
		font-size: 30rpx !important;
	}

	button::after {
		border-color: rgba(0, 0, 0, 0);
	}

	.uni-swiper-slides {
		height: 400rpx;
	}

	uni-swiper {
		height: 400rpx !important;
		z-index: 999999;
		background-color: #fff;
	}

	.hidden {
		display: none;
	}

	z-index8 {
		z-index: 8;
	}

	.zanwu {
		width: 100%;
		line-height: 240rpx;
		text-align: center;
		font-size: 28rpx;
		color: #999;
	}

	view {
		box-sizing: border-box;
		font-family: PingFang SC;
	}

	.dis_flex {
		/*  #ifndef APP-PLUS-NVUE  */
		display: flex;
		/*  #endif  */
	}

	.dis_flex_c {
		/*  #ifndef APP-PLUS-NVUE  */
		display: flex;
		/*  #endif  */
		flex-direction: column;
	}

	.aic {
		align-items: center;
	}

	.ais {
		align-items: stretch;
	}

	.aift {
		align-items: flex-start;
	}

	.aife {
		align-items: flex-end;
	}

	.ju_a {
		justify-content: space-around;
	}

	.ju_b {
		justify-content: space-between;
	}

	.ju_c {
		justify-content: center;
	}

	.flex_1 {
		flex: 1;
	}

	.flex_0 {
		flex: none;
	}

	.oh1 {
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp: 1;
		-webkit-box-orient: vertical;
	}

	.oh2 {
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp: 2;
		-webkit-box-orient: vertical;

	}

	view {
		word-break: break-all;

		word-wrap: break-word;
	}

	.oh3 {
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp: 3;
		-webkit-box-orient: vertical;
	}

	.oh4 {
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp: 4;
		-webkit-box-orient: vertical;
	}

	.data_last {
		line-height: 100rpx;
		text-align: center;
		width: 100%;
		font-size: 24rpx;
		color: #666;
	}

	.data_null {
		width: 480upx;
		height: 480upx;
		margin-top: 260upx;
	}



	.xmfwb_box image,
	.xmfwb_box img,
	.xmfwb_box table,
	rich-text p,
	rich-text img,
	rich-text table {
		max-width: 100% !important;
	}

	.xcx_fwb_img {
		max-width: 100% !important;
	}

	.loading_def {
		position: fixed;
		top: 0;
		bottom: 0;
		right: 0;
		left: 0;
		display: flex;
		align-items: center;
		justify-content: center;
		background: #fff;
	}

	.loading_def_img {
		width: 200rpx !important;
		height: 200rpx !important
	}

	.minh100 {
		width: 100%;
		min-height: 100vh;
		background: #fff;
		box-sizing: border-box;
	}


	.scroll_x {
		width: 100%;
		white-space: nowrap;
	}
	
	
	
	//我自己的
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
	//超部分显示省略号
	.go-beyond-no-flex {
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
		overflow: hidden;
	}
	
	.go-beyond-flex {
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}
	//处理兼容
	.compatibleProcessing{
		box-sizing: content-box;
		padding-bottom: constant(safe-area-inset-bottom);
		/* 兼容 iOS < 11.2 */
		padding-bottom: env(safe-area-inset-bottom);
		/* 兼容 iOS >= 11.2 */
	}
	
</style>
