<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="车辆绑定" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<car-cell cellColor="#22282F">
					<view slot="left"><span class="num">SN码</span></view>
					<view slot="center">
						<input class="newPhone" type="text" placeholder="见《快速安装使用说明》" value="" maxlength="15" />
					</view>
					<view slot="right"><text @click="gotoScan" class="scan cuIcon cuIcon-scan"></text></view>
				</car-cell>
				<view class="btn cu-btn block radius" @click="gotoBindSuccess">
					<text class="bind">确认绑定</text>
				</view>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'BindMedia',
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
			gotoBindSuccess() {
				uni.navigateTo({
					url: '/pages/my/bindmedia/success/index'
				})
			},
			gotoScan() {
				// uni.navigateTo({
				// 	url: '/pages/my/bindmedia/scan/index'
				// })
				uni.scanCode({
					success: function(res) {
						console.log(res)
						console.log('条码类型：' + res.scanType);
						console.log('条码内容：' + res.result);
					}
				});
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
			.num {
				font-size: 28rpx;
			}
			.newPhone {
				margin: 0 28rpx;
				margin-left: 110rpx;
				font-size: 28rpx;
			}
			.scan {
				color: #FFFFFF;
				font-size: 40rpx;
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
