<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="购买" backColor="#191E24">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
			<view slot="right">
				<view class="cart">
					<image src="/static/images/icons/mall/cartCar.png" mode="scaleToFill"></image>
				</view>
				<text class="shopNum">7</text>
			</view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<car-list-cell :cellListStyle="cellListStyle" cellImg="/static/images/icons/mall/shopName.jpg">
					<view slot="topInfo">
						<text class="topTitle">本期话题：你觉得那哪个配件是你爱车上的“点睛之笔”</text>
					</view>
					<view slot="btmInfo">
						<text class="btmIndexTitle">￥ 5699.00</text>
					</view>
				</car-list-cell>
				<car-cell cellColor="#22282F" class="cellList">
					<view slot="left"><text class="email">属性</text></view>
					<view slot="center">
						<input class="email" disabled type="text" value="白色" maxlength="20" />
					</view>
				</car-cell>
				<view class="address">
					<view class="topAd">
						<text>收货地址</text>
						<text class="topAdChange">修改</text>
					</view>
					<view class="btmAd">
						<view class="info">
							<text class="location cuIcon cuIcon-location"></text><text class="userName">大黄鸭</text><text
								class="userPhone">159****3344</text>
						</view>
						<view class="area">
							<text class="pos">地址：</text><text class="areaName">四川省成都市锦江区三圣乡花卉市场</text>
						</view>
					</view>
				</view>
				<view class="shopCost">
					<view class="costOne">
						<text>商品总额</text>
						<text>￥220.00</text>
					</view>
					<view class="costOne">
						<text>运费</text>
						<text>￥12.00</text>
					</view>
					<view class="costTwo">
						<text>应付款</text>
						<text class="shouldCost">￥220.00</text>
					</view>
				</view>
				<view class="btmOptions">
					<text class="cost">￥ 5699.00</text>
					<text class="pay">立即支付</text>
				</view>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'FastPay',
		data() {
			return {

			}
		},
		computed: {
			Style() {
				let style = {
					'height': "calc(100vh - " + this.CustomBar * 2 + 'rpx' + ")"
				}
				return style
			},
			cellListStyle() {
				let style = {
					'height': '180rpx'
				}
				return style
			}
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

		.cart {
			image {
				width: 42rpx;
				height: 42rpx;
			}
		}
		.shopNum {
			position: absolute;
			right: -10rpx;
			top: -8rpx;
			font-size: 20rpx !important;
			background-color: #EC3E55;
			padding: 2rpx 12rpx;
			border-radius: 14rpx;
		}

		.content {
			width: 100%;
			height: 100%;
			position: relative;
			padding: 20rpx 32rpx;
			padding-top: 60rpx;
			background-color: #191E24;

			.topTitle {
				// 超过两行自动省略号
				overflow: hidden;
				text-overflow: ellipsis;
				display: -webkit-box;
				-webkit-box-orient: vertical;
				-webkit-line-clamp: 2;
				font-size: 32rpx;
				color: #FFFFFF;
			}

			.btmIndexTitle {
				font-size: 32rpx;
				color: #FFFFFF;
			}

			.car-list-cell {
				padding: 0;
				margin-bottom: 40rpx;
				background-color: #191E24 !important;
			}

			.email {
				text-align: right;
				font-size: 28rpx;
				color: #FFFFFF;
			}

			.cellList {
				border-radius: 12rpx;
			}
			.address {
				margin-top: 20rpx;
				padding: 32rpx;
				background-color: #22282F;
				border-radius: 12rpx;

				.topAd {
					display: flex;
					justify-content: space-between;
					align-items: center;
					font-size: 28rpx;
					color: #FFFFFF;

					.topAdChange {
						color: #2A77FF;
					}
				}

				.btmAd {
					position: relative;
					margin-top: 24rpx;

					.info {
						font-size: 26rpx;
						color: #FFFFFF;
						margin-bottom: 16rpx;

						.location {
							margin-right: 16rpx;
						}

						.userName {
							margin-right: 32rpx;
						}
					}

					.area {
						color: #69707C;
						font-size: 24rpx;

						.pos {
							margin-left: 42rpx;
						}

					}
				}
			}

			.shopCost {
				margin-top: 40rpx;
				color: #FFFFFF;
				font-size: 26rpx;

				.costOne {
					display: flex;
					justify-content: space-between;
					align-items: center;
					margin-bottom: 30rpx;
				}

				.costTwo {
					display: flex;
					justify-content: flex-end;
					align-items: center;

					.shouldCost {
						font-size: 32rpx;
						margin-left: 20rpx;
					}
				}
			}
			.btmOptions {
				position: fixed;
				bottom: 0;
				left: 0;
				right: 0;
				height: 100rpx;
				background-color: #2E343C;
				color: #FFFFFF;
				font-size: 30rpx;
				display: flex;
				justify-content: space-between;
				align-items: center;
				.cost {
					margin-left: 32rpx;
					color: #EC3E55;
					font-size: 32rpx;
				}
				.pay {
					padding: 30rpx 58rpx 28rpx 58rpx;
					background-color: #EC3E55;
				}
			}
		}
	}
</style>
