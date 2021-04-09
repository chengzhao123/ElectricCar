<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="更换手机号" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<view class="cTitle">请输入新手机号</view>
				<car-cell cellColor="#22282F">
					<view slot="left"><span class="num">+86</span><span class="line"></span></view>
					<view slot="center">
						<input class="newPhone" type="text" placeholder="手机号" value="15928953344" maxlength="15" />
					</view>
					<view slot="right"><image class="dela" src="/static/images/icons/my/del.png" mode="widthFix" @click="deleteValue"></image></view>
				</car-cell>
				<view class="btn cu-btn block radius" @click="gotoSendPhone">
					<text class="bind">发送验证码</text>
				</view>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'NewPhone',
		data() {
			return {
				
			}
		},
		computed:{
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
		methods:{
			back() {
				uni.navigateBack()
			},
			deleteValue() {
				console.log('删除')
			},
			gotoSendPhone() {
				uni.navigateTo({
					url: '/pages/my/info/sendPhone/index'
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
			position: relative;
			padding: 32rpx 0;
			.dela {
				width: 32rpx;
			}
			.cTitle {
				font-size: 28rpx;
				color: #69707C;
				margin-bottom: 30rpx;
				padding-left: 32rpx;
			}
			.num {
				font-size: 32rpx;
			}
			.line {
				margin-left: 28rpx;
				border-right: 1px solid #343B43;
			}
			.newPhone {
				margin: 0 28rpx;
				font-size: 32rpx;
			}
			.btn {
				box-sizing: border-box;
				margin: 60rpx 32rpx;
				height: 100rpx;
				background-color: #2A77FF;
				.bind {
					font-size: 32rpx;
					color: #FFFFFF;
				}
			}
		}
	}
</style>
