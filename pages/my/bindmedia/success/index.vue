<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" backColor="#191E24">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<image class="successImg" src="/static/images/icons/my/logo.png" mode="widthFix" />
				<view class="successInfo">
					<text class="okicon cuIcon cuIcon-roundcheckfill"></text>
					<text class="bind">绑定成功</text>
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
		background-color: #191E24;
	
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
				justify-content: center;
				align-items: center;
				color: #FFFFFF;
				margin: 40rpx 0 80rpx 0;
				.okicon {
					font-size: 42rpx;
					color: #19C038;
					margin-right: 20rpx;
					margin-top: 10rpx;
				}
				.bind {
					font-size: 32rpx;
					color: #FFFFFF;
				}
			}
		}
	}
</style>
