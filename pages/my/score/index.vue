<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="我的积分">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
			<view slot="right"><text class="cuIcon cuIcon-settings"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<view class="header">
					<image class="scoreImg" src="/static/images/icons/my/logo.png" mode="widthFix"></image>
					<text class="scoreNum">305</text>
				</view>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'Score',
		data() {
			return {
				
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
		},
		
	}
</script>

<style lang="scss" scoped>
	.mf {
		position: absolute;
		top: 0;
		right: 0;
		bottom: 0;
		left: 0;
		background-color: #D8D8D8;
		.content {
			width: 100%;
			height: 100%;
			.header {
				padding: 48rpx 32rpx;
				width: 100%;
				background-color: #22282F;
				display: flex;
				justify-content: flex-start;
				align-items: center;
				.scoreImg {
					width: 64rpx;
					height: 64rpx;
					border-radius: 50%;
					margin-right: 40rpx;
				}
				.scoreNum {
					font-size: 52rpx;
					color: #FFFFFF;
				}
			}
		}
	}
</style>
