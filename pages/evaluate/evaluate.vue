<template>
	<view class="evaluate">
		<!-- 自定义导航 -->
		<uni-nav-bar fixed statusBar :title="title" class="status-title" @clickLeft="back">
			<uni-icons slot="left" type="arrowleft" class="status-icon" size="17"></uni-icons>
		</uni-nav-bar>
		<evaluate :evaluate="evaluate" isEvaluate=false></evaluate>
	</view>
</template>

<script>
	import evaluate from '../../components/evaluate/evaluate.vue'
	export default {
		components:{
			evaluate
		},
		data() {
			return {
				title: "全部评价",
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
			};
		},
		methods: {
			back() {
				uni.navigateBack({
					delta: 1
				})
			}
		}
	}
</script>

<style lang="scss">
	.evaluate {
		.status-title {
			font-size: 34rpx;
			font-family: PingFang;
			font-weight: bold;
			color: #000000;

			.status-icon {
				font-size: 30rpx;
			}
		}
		.evaluateView{
			width: 750rpx;
			margin: -5rpx 60rpx 0 60rpx;
			height: auto !important;
			box-shadow: none;
			background-color: #ffffff;
			padding: 0;
		}
	}

	//修改第三方组件样式
	/deep/ .uni-navbar--border.data-v-6bda1a90 {
		border: none !important;
	}
</style>
