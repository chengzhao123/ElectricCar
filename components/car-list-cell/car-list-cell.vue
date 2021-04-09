<template>
	<view class="car-list-cell" @click="itemClick">
		<slot name="topLR"/>
		<view class="car-list-cellTop" :style="[cellListStyle]">
			<image class="car-list-cellImg radius" :src="cellImg" mode="heightFix" />
			<view class="car-list-cellRight">
				<view class="car-list-cellRightTop">
					<slot name="topInfo" />
				</view>
				<view class="car-list-cellRightBtm">
					<slot name="btmInfo" />
				</view>
			</view>
		</view>
		<slot name="btmRight"/>
	</view>
</template>

<script>
	export default {
		name: 'car-list-cell',
		props: {
			cellImg: {
				type: String,
				default : '/static/images/icons/mall/shopName.jpg'
			},
			cellListStyle: {
				type: Object,
				default: function() {
					return {}
				}
			}
		},
		computed: {
			
		},
		methods: {
			itemClick() {
				this.$emit('itemClick')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.car-list-cell {
		position: relative;
		padding: 40rpx 32rpx;
		background-color: #22282F;
		margin-top: 20rpx;
		.car-list-cellTop {
			position: relative;
			display: flex;
			height: 140rpx;
			justify-content: space-between;
			align-items: center;
			.car-list-cellImg {
				height: 100%;
			}
			.car-list-cellRight {
				flex: 1;
				height: 100%;
				margin-left: 32rpx;
				display: flex;
				flex-direction: column;
				align-items: flex-start;
				justify-content: space-between;
			}
		}
	}
</style>
