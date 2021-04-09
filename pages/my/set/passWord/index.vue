<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="手机号" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<view class="topArea">					
					<text class="phoneNum">+86 15928953344</text>
					<text class="change">即将发送验证码至您的手机号</text>
				</view>
				
				<view class="btn cu-btn block radius" @click="gotoNewPassWd">
					<text class="bind">发送验证码</text>
				</view>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'PassWordIndex',
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
			},
			gotoNewPassWd() {
				uni.navigateTo({
					url: '/pages/my/set/sendPassWd/index'
				})
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
			padding: 72rpx;
			.topArea {
				height: 240rpx;
				display: flex;
				flex-direction: column;
				justify-content: flex-end;
				align-items: center;
				.phoneImg {
					width: 50rpx ;
					height: 100rpx ;
				}
				.change {
					font-size: 28rpx;
					color: #69707C;
					margin: 28rpx 0;
				}
				.phoneNum {
					font-size: 64rpx;
					margin: 20rpx 0 0 0;
					color: #FFFFFF;
					font-weight: bold;
				}
			}
			.btn {
				height: 100rpx;
				background-color: #2A77FF;
				margin-top: 30rpx;
				.bind {
					font-size: 32rpx;
					color: #FFFFFF;
				}
			}
		}
	}
</style>
