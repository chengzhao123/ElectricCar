<template>
	<view class="car-cell-box" :style="{'background-color': cellColor}" :class="marginTB ? 'car-cell-margin' : '' " >
		<view class="car-cell" @click="jump">
			<view class="car-cell-left">
				<slot name="left"></slot>
			</view>
			<view class="car-cell-center">
				<slot name="center"></slot>
			</view>
			<view class="car-cell-right">
				<slot name="right"></slot>
				<text v-if="isArrow" class="cuIcon cuIcon-right margin-left"></text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'car-cell',
		data (){
			return {
				
			}
		},
		props: {
			isArrow: {
				type: Boolean,
				default: false
			},
			marginTB: {
				type: Boolean,
				default: false
			},
			cellColor: {
				type: String,
				default: '#FFFFFF'
			}
		},
		methods: {
			jump() {
				this.$emit('jump')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.car-cell-margin {
		margin-bottom: 20rpx;
	}
	.car-cell-box {
		padding: 32rpx;
		background-color: #22282F;
		border-bottom: 1px solid #191E24;
		.car-cell {
			display: flex;
			justify-content: space-between;
			align-items: center;
			font-size: 28rpx;
			.car-cell-left {
				color: #FFFFFF;
				white-space: nowrap;
			}
			.car-cell-center,.car-cell-right {
				color: #69707C;
			}
			.car-cell-center {
				flex: 1;
				color: #FFFFFF;
			}
			.car-cell-right {
				display: flex;
				justify-content: space-between;
				align-items: center;
				font-size: 32rpx;
				.margin-left {
					margin-left: 12rpx;
				}
			}
		}
	}
</style>
