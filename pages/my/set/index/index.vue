<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="设置" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<car-cell isArrow cellColor="#22282F" marginTB @jump="gotoPwd">
					<view slot="left">修改密码</view>
				</car-cell>
				<car-cell isArrow cellColor="#22282F" @jump="setPhone">
					<view slot="left">清空缓存</view>
					<view slot="right"><text>1.5MB</text></view>
				</car-cell>
				<car-cell isArrow cellColor="#22282F" @jump="setEmail" marginTB>
					<view slot="left">关于</view>
					<view slot="right"><text>1.0.0</text></view>
				</car-cell>
				<car-cell cellColor="#22282F">
					<view slot="left">退出登录</view>
				</car-cell>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'Set',
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
			gotoPwd() {
				uni.navigateTo({
					url: '/pages/my/set/passWord/index'
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
			padding: 20rpx 0;
		}
	}
</style>
