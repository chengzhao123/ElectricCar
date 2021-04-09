<template>
	<view class="car-shop-cart" :style="[shopCart]">
		<view class="car-shop-content">
			<view class="car-shop-left">
				<view class="collectCar" @click="favarCart">
					<text class="iconType cuIcon cuIcon-favor"></text>
					<text class="iconTitle">收藏</text>
				</view>
				<view class="shopCar" @click="cartCage">
					<text class="iconType cuIcon cuIcon-cart"></text>
					<text class="iconTitle">购物车</text>
				</view>
			</view>
			<view class="car-shop-right">
				<view class="addCar" @click="addCar">
					<text>加入购物车</text>
				</view>
				<view class="buyCar" @click="fastPay">
					<text>立即购买</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		nae:'car-shop-cart',
		props:{
			shopCart: {
				type: Object,
				default: function() {
					return {
						'height': '100rpx',
						'background-color': '#2E343C'
					}
				}
			}
		},
		data() {
			return {
				
			}
		},
		methods: {
			favarCart() {
				this.$emit('favarCart')
			},
			cartCage() {
				this.$emit('cartCage')
			},
			addCar() {
				this.$emit('addCar')
			},
			fastPay() {
				this.$emit('fastPay')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.car-shop-cart {
		position: absolute;
		left: 0;
		right: 0;
		z-index: 9999;
		.car-shop-content {
			position: relative;
			display: flex;
			justify-content: space-between;
			align-items: center;
			height: 100%;
			.car-shop-left {
				display: flex;
				justify-content: space-around;
				flex: 1;
				align-items: center;
				background-color: #2E343C;
				height: 100%;
				.collectCar, .shopCar {
					display: flex;
					flex-direction: column;
					justify-content: space-between;
					align-items: center;
					.iconType {
						color: #FFFFFF;
						font-size: 32rpx;
					}
					.iconTitle {
						font-size: 22rpx;
						color: #69707C;
					}
				}
			}
			.car-shop-right {
				height: 100%;
				display: flex;
				justify-content: space-between;
				align-items: center;
				width: 472rpx;
				.addCar, .buyCar {
					flex: 1;
					display: flex;
					justify-content: center;
					align-items: center;
					height: 100%;
					text {
						font-size: 30rpx;
						color: #FFFFFF;
					}
				}
				.addCar {
					background-color: #ECA33E;
				}
				.buyCar {
					background-color: #EC3E55;
				}
			}
		}
	}
</style>
