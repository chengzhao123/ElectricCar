<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="购物车" backColor="#191E24">
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
				<car-cell cellColor="#22282F" class="cellList">
					<view slot="left"><text class="num">购物数量：{{num}}</text></view>
					<view slot="right">
						<view @click="gotoWatch">
							<text class="opreateSet" v-if="isSet">取消</text>
							<text class="opreate" v-else>管理</text>
						</view>
					</view>
				</car-cell>

				<view class="cartBox" v-for="(item, index) in 10" :key="index">
					<view class="l">
						<text v-if="1 == 1" class="chooseAll cuIcon cuIcon-roundcheckfill"></text>
						<text v-else class="choose cuIcon cuIcon-round"></text>
					</view>
					<view class="r">
						<view class="cartImg">
							<image src="/static/images/icons/mall/shopName.jpg" mode="scaleToFill" />
						</view>
						<view class="methods">
							<text class="title">上班出行顶配电摩NQi顶配上班出行顶配电摩NQi顶配上班出行顶配电摩NQi顶配</text>
							<text class="color">属性：白色</text>
							<view class="addRem">
								<text class="costOne">￥ 5699.00</text>
								<view class="xuanxiang">
									<text class="rem">−</text>
									<text class="evnum">{{1}}</text>
									<text class="add">+</text>
								</view>
							</view>
						</view>
					</view>
				</view>

				<!-- 底部选择栏 -->
				<view class="btmOptionstwo" v-if="isSet">
					<view class="leftOptionstwo">
						<view class="l">
							<text v-if="1 == 1" class="chooseAll cuIcon cuIcon-roundcheckfill"></text>
							<text v-else class="choose cuIcon cuIcon-round"></text>
							<text class="btnChoose" @click="changeAll">全选</text>
							<text class="btnChoose"> ({{num}})</text>
						</view>
					</view>
					<text class="orderFavor">收藏</text>
					<text class="orderDel">删除</text>
				</view>
				<!-- 底部选择栏 -->
				<view class="btmOptions" v-else>
					<view class="leftOptions">
						<view class="l">
							<text v-if="1 == 1" class="chooseAll cuIcon cuIcon-roundcheckfill"></text>
							<text v-else class="choose cuIcon cuIcon-round"></text>
							<text class="btnChoose" @click="changeAll">全选</text>
							<text class="btnChoose"> ({{num}})</text>
						</view>
						<text class="cost">￥ 5699.00</text>
					</view>
					<text class="orderFast">立即下单</text>
				</view>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'CartCar',
		data() {
			return {
				num: 2,
				isSet: false
			}
		},
		computed: {
			Style() {
				let style = {
					'height': "calc(100vh - " + this.CustomBar * 2 + 'rpx' + ")"
				}
				return style
			},
		},
		methods: {
			back() {
				uni.navigateBack()
			},
			changeAll() {
				console.log('点击了全选')
			},
			gotoWatch() {
				// uni.navigateTo({
				// 	url: '/pages/mall/cartCarSet/index'
				// })
				this.isSet = !this.isSet
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
			padding: 20rpx 32rpx 120rpx 32rpx;

			.cellList {
				// margin-top: 20rpx;
				border-radius: 12rpx;
				
				.num {
					font-size: 28rpx;
					color: #FFFFFF;
				}

				.opreate {
					box-sizing: border-box;
					font-size: 28rpx;
					color: #2A77FF;
					padding: 12rpx 24rpx;
					border: 1px solid #2A77FF;
					border-radius: 30rpx;
					background-color: transparent;
				}

				.opreateSet {
					font-size: 28rpx;
					color: #FFFFFF;
					padding: 12rpx 24rpx;
					border: 1px solid #FFFFFF;
					border-radius: 30rpx;
					background-color: transparent;
				}
			}

			.cartBox {
				position: relative;
				padding: 32rpx 28rpx;
				margin-top: 20rpx;
				background-color: #22282F;
				border-radius: 12rpx;
				display: flex;
				justify-content: space-between;
				align-items: center;

				.l {
					margin-right: 28rpx;

					.chooseAll {
						font-size: 36rpx;
						color: #2A77FF;
					}

					.choose {
						font-size: 36rpx;
						color: #838A93;
					}
				}

				.r {
					flex: 1;
					width: 0;
					display: flex;
					justify-content: space-between;
					align-items: center;

					.cartImg {
						width: 154rpx;
						height: 148rpx;
						image {
							width: 100%;
							height: 100%;
							border-radius: 12rpx;
						}
					}

					.methods {
						margin-left: 24rpx;
						flex: 1;
						height: 100%;
						overflow: hidden;

						.title {
							position: relative;
							display: inline-block;
							width: 100%;
							font-size: 28rpx;
							color: #FFFFFF;
							overflow: hidden;
							text-overflow: ellipsis;
							white-space: nowrap;
							margin-bottom: 12rpx;
						}

						.color {
							display: inline-block;
							background-color: #2E343C;
							color: #838A93;
							border: 1px solid #2E343C;
							border-radius: 30rpx;
							padding: 12rpx 20rpx;
							font-size: 24rpx;
							line-height: 100%;
							margin-bottom: 14rpx;
						}

						.addRem {
							display: flex;
							justify-content: space-between;
							align-items: center;
							font-size: 32rpx;

							.costOne {
								color: #EC3E55;
							}

							.xuanxiang {
								display: flex;
								justify-content: center;
								align-items: center;

								.rem,
								.add {
									display: inline-block;
									font-size: 32rpx;
									text-align: center;
									width: 36rpx;
									height: 36rpx;
									border-radius: 50%;
									overflow: hidden;
								}

								.rem {
									position: relative;
									background-color: #2E343C;
									color: rgba(216, 216, 216, .3);
								}

								.add {
									color: #FFFFFF;
									background-color: #2A77FF;
								}

								.evnum {
									margin: 0 32rpx;
									color: #838A93;
									font-size: 28rpx;
								}
							}
						}
					}
				}
			}

			.btmOptionstwo {
				position: fixed;
				bottom: 0;
				left: 0;
				right: 0;
				height: 100rpx;
				background-color: #2E343C;
				color: #FFFFFF;
				display: flex;
				justify-content: space-between;
				align-items: center;

				.orderFavor,
				.orderDel {
					font-size: 30rpx;
					color: #FFFFFF;
					border-radius: 12rpx;
					padding: 14rpx 78rpx;
				}

				.orderFavor {
					background-color: #2A77FF;
				}

				.orderDel {
					margin-left: 24rpx;
					margin-right: 32rpx;
					background-color: #191E24;
				}

				.leftOptionstwo {
					flex: 1;
					padding: 0 32rpx;
					display: flex;
					justify-content: space-between;
					align-items: center;

					.l {
						display: flex;
						align-items: center;

						.chooseAll {
							font-size: 36rpx;
							color: #2A77FF;
						}

						.choose {
							font-size: 36rpx;
							color: #838A93;
						}

						.btnChoose {
							line-height: 100%;
							margin-left: 18rpx;
							font-size: 28rpx;
							color: #FFFFFF;
						}
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
				display: flex;
				justify-content: space-between;
				align-items: center;

				.orderFast {
					font-size: 30rpx;
					background-color: #EC3E55;
					padding: 30rpx 58rpx 28rpx 58rpx;
				}

				.leftOptions {
					flex: 1;
					padding: 0 32rpx;
					display: flex;
					justify-content: space-between;
					align-items: center;

					.l {
						display: flex;
						align-items: center;

						.chooseAll {
							font-size: 36rpx;
							color: #2A77FF;
						}

						.choose {
							font-size: 36rpx;
							color: #838A93;
						}

						.btnChoose {
							line-height: 100%;
							margin-left: 18rpx;
							font-size: 28rpx;
							color: #FFFFFF;
						}
					}

					.cost {
						color: #EC3E55;
						font-size: 32rpx;
					}
				}
			}

		}
	}
</style>
