<template>
	<view class="car-list-shop-cell radius" @click="shopIndex">
		<image class="shopImg" :src="shopImg" mode="scaleToFill"></image>
		<view class="midTitle">
			<slot name="midTitle" />
		</view>
		<view class="btmTitle">
			<view class="btmOne">
				<slot name="btmOne" />
			</view>
			<view class="btmTwo">
				<slot name="btmTwo" />
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'car-list-shop-list',
		props: {
			shopImg: {
				type: String,
				default: '/static/images/icons/mall/shopName.jpg'
			}
		},
		methods: {
			shopIndex() {
				this.$emit('shopItemIndex')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.car-list-shop-cell {
		width: 334rpx;
		position: relative;
		// padding: 32rpx;
		margin-bottom: 20rpx;
		overflow: hidden;
		background-color: #22282F;
		.shopImg {
			width: 334rpx;
			height: 370rpx;
			border-radius: 12rpx;
		}
		.midTitle {
			padding: 24rpx;
		}
		.btmTitle {
			padding:0 24rpx 24rpx 24rpx;
			.btmOne {
				
			}
			.btmTwo {
				height: 34rpx;
			}
		}
		
	}
</style>
