<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<image class="successImg" src="/static/images/icons/my/logo.png" mode="widthFix" />
				<view class="successInfo">
					<text>提交成功，我们已收到您的报修</text>
					 <text>请耐心等待网点与您联系</text>
				</view>
				<view class="btn cu-btn block radius">
					<text class="bind">返回首页 {{time}}s</text>
				</view>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'OnlineXiuSuccess',
		data() {
			return {
				time: 6
			}
		},
		computed: {
			Style() {
				let style = {
					// #ifdef APP-PLUS || H5
					'height': "calc(100vh - " + this.CustomBar * 2 + 'rpx' + ")"
					// #endif
					// #ifdef MP-WEIXIN
					'height': "calc(100vh - 100rpx - " + this.CustomBar * 2 + 'rpx' + ")"
					// #endif
				}
				return style
			},
		},
		methods: {
			back() {
				uni.navigateBack()
			}
		}
		
	}
</script>

<style lang="scss" scoped>
	.mf {
		position: absolute;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		background-color: #22282F;
	
		.content {
			width: 100%;
			height: 100%;
			padding: 32rpx;
			flex-direction: column;
			display: flex;
			align-items: center;
			justify-content: flex-start;
			padding-top: 250rpx;
			.successImg {
				width: 140rpx;
			}
			.successInfo {
				display: flex;
				flex-direction: column;
				justify-content: space-between;
				align-items: center;
				color: #FFFFFF;
				margin: 40rpx 0 80rpx 0;
			}
			.btn {
				height: 100rpx;
				background-color: transparent;
				border: 1px solid #2A77FF;
				padding: 0 100rpx;
				.bind {
					font-size: 32rpx;
					color: #2A77FF;
				}
			}
		}
	}
</style>
