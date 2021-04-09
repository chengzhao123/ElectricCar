<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="收货地址" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<car-cell isArrow cellColor="#22282F" class="cell" @jump="clickAdr">
					<view slot="left">选择城市</view>
					<view slot="right">
						<text class="areaName">{{address}}</text>
					</view>
				</car-cell>
				<view class="detail">
					<view class="dTitle">详细街道</view>
					<textarea class="area" maxlength="200" placeholder="请输入详细地址"></textarea>
				</view>
				<car-cell cellColor="#22282F" class="cell">
					<view slot="left">收货人</view>
					<view slot="right"><input class="input" type="text" value="鸭先生" maxlength="8" /></view>
				</car-cell>
				<car-cell cellColor="#22282F" class="cell">
					<view slot="left">手机号</view>
					<view slot="right"><input class="input" type="text" value="159 2895 3344" maxlength="15" /></view>
				</car-cell>
				<view class="btn cu-btn block radius">
					<text class="bind">保存</text>
				</view>
				<w-picker ref="picker" :visible.sync="visible" mode="region" :value="address" current @confirm="onConfirm($event,'date')"
					@cancel="onCancel"></w-picker>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'Address',
		data() {
			return {
				address: '',
				visible: false
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
			onConfirm(e) {
				this.address = e.result
			},
			onCancel() {
				this.$refs.picker.hide()
			},
			clickAdr() {
				this.$refs.picker.show()
			},
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
			padding: 20rpx;
			.detail {
				width: 100%;
				height: 340rpx;
				padding: 30rpx;
				border-radius: 16rpx;
				font-size: 28rpx;
				color: #FFFFFF;
				background-color: #22282F;
				margin: 20rpx 0;
				.dTitle {
					margin-bottom: 20rpx;
				}
				.area {
					width: 100%;
				}
			}
			.cell {
				border-radius: 16rpx;
				.areaName {
					font-size: 28rpx;
					color: #69707C;
					white-space: nowrap;
				}
				.input {
					color: #FFFFFF;
					text-align: right;
				}
			}
			.btn {
				height: 100rpx;
				background-color: #2A77FF;
				margin-top: 20rpx;
				.bind {
					font-size: 32rpx;
					color: #FFFFFF;
				}
			}
		}
	}
</style>
