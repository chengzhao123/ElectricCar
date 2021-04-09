<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="商城" backColor="#191E24">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
			<view slot="right">
				<view class="cart">
					<image src="/static/images/icons/mall/cartCar.png" mode="scaleToFill"></image>
				</view>
				<text class="shopNum">7</text>
			</view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style" @refresh="onRefresh" :triggered="triggered" isCanRefresher>
			<view class="content">
				<view class="shopImg">
					<image src="/static/images/icons/mall/shopName.jpg" mode="aspectFill" />
				</view>
				<view class="topDetail">
					<text class="topTitle">上班出行 顶配电摩 NQi顶配版理论续航800km顶配电摩 NQi顶配版理论续航800k</text>
					<text class="topInfo">在众多电动车品牌中,新日和雅迪都是家喻户晓的头部品牌。通常在选购电动车时,很多人都会纠结是选新日还是选雅迪,希望今天这篇文章,对大家有所帮助。</text>
					<text class="topMoney">￥ 5699.00</text>
					<view class="topPreInfo">
						<text>原价：￥7699.00</text>
						<text>库存：24</text>
						<text>销量：5552</text>
					</view>
				</view>
				<car-cell isArrow cellColor="#22282F">
					<view slot="left"><text class="email">属性</text></view>
					<view slot="center">
						<input @click="changePop" class="email" disabled type="text" value="白色" maxlength="20" />
					</view>
				</car-cell>
				<view class="shopCartInfo">
					<view class="cartInfo">产品详情</view>
					<view class="cartInfoArea"></view>
				</view>
				<view class="shopWillLike">
					<view class="cartLikeInfo">猜你喜欢</view>
					<view class="cartLikeList">
						<car-list-shop-cell v-for="(item, index) in 5" :key='index' @shopItemIndex="maylike" shopImg="/static/images/icons/mall/shopName.jpg">
							<view slot="midTitle">
								<text class="midTitle">上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行 顶配电摩 NQi顶配版理论续航800km</text>
							</view>
							<view slot="btmOne">
								<text class="btmTwoTitle">￥ 5699.00</text>
							</view>
							<view slot="btmTwo">
								<text class="btmTwoPreTitle" v-if="index % 2 == 0">原价￥ 2123.00</text>
							</view>
						</car-list-shop-cell>
					</view>
				</view>
				
			</view>
		</car-container>
		<view class="rightIcon">
			<view class="service"><text class="cuIcon cuIcon-service"></text></view>
			<view class="top"><text class="cuIcon cuIcon-top"></text></view>
		</view>
		<car-shop-cart :shopCart="shopCartStyle" @fastPay="fastPay"></car-shop-cart>
		<!-- 底部弹出属性选择 -->
		<view class="cu-modal bottom-modal oneModal" :class="showModal ?'show':''" @click.stop="showModal = false">
		  <view class="cu-dialog typeDialog" @click.stop="">
			<text class="closeBtn cuIcon cuIcon-close"></text>
			<view class="diaCont">
				<view class="dialogInfo">
					<view class="dialogTop">
						<view class="diaImgArea">
							<image class="dialogImg" src="/static/images/icons/mall/shopName.jpg" mode="scaleToFill" />
						</view>
						<view class="dialogRight">
							<view class="diaShopTitle">班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上</view>
							<view class="diaShopCost">￥ 5699.00</view>
							<view class="diaShopSave">库存：44</view>
						</view>
					</view>
					<view class="cartColor">
						<view class="colorTitle">颜色</view>
						<view class="colorType">
							<view v-for="(item, index) in 10"
								:key="index"
								class="colorItem"
								:class="currentColorIndex == index ? 'activeColor' : '' "
								@click="currentColorIndex = index"
							>
								<text class="colorName">颜色{{item}}</text>
							</view>
						</view>
					</view>
					<view class="cartCount">
						<view class="countTitle">数量</view>
						<view class="inputCount">
							<text class="countRem" :class="countNum == 0 ? 'lastCount' : '' ">-</text>
							<input class="countNum" type="text" v-model="countNum" maxlength="5" />
							<text class="countAdd">+</text>
						</view>
					</view>
				</view>
			</view>
			
		  </view>
		</view>

	</view>
</template>

<script>
	export default {
		name: 'ShopIndex',

		data() {
			return {
				currentColorIndex: 0,
				countNum: 0,
				triggered: false,
				showModal: false
			}
		},
		computed: {
			Style() {
				let style = {
					'height': "calc(100vh - " + this.CustomBar * 2 + 'rpx' + ")"
				}
				return style
			},
			shopCartStyle() {
				let style = {
					'position': 'fixed',
					'bottom': '0',
					'height': '100rpx',
					'background-color': '#2E343C'
				}
				return style
			}
		},
		methods: {
			back() {
				uni.navigateBack()
			},
				
			maylike() {
				console.log('---')
			},
			initData() {
				setTimeout(() => {
					this._refreshing = false
					this.triggered = false
					uni.showToast({
						title: '刷新成功',
						icon: 'none',
						duration: 1000
					})
				}, 1000)
			},
			fastPay() {
				uni.navigateTo({
					url:'/pages/mall/fastPay/index'
				})
			},
			changePop() {
				uni.pageScrollTo({
					scrollTop: 0,
					duration: 200
				});
				this.showModal = true
			},
			onRefresh() {
				if (this._refreshing) return
				this._refreshing = true;
				this.triggered = true;
				this.initData();
			}
		}
	}
</script>

<style lang="scss" scoped>
	.rightIcon {
		position: absolute;
		// z-index: 9;
		right: 32rpx;
		bottom: 140rpx;
		.service, .top {
			padding: 22rpx 26rpx;
			border-radius: 50%;
			background-color: #FFFFFF;
			text {
				font-size: 40rpx;
				color: #000000;
			}
		}
		.top {
			margin-top: 22rpx;
		}
	}
	// 修改弹窗样式
	.oneModal  {
		bottom: 100rpx !important;
		.typeDialog {
			border-top-right-radius: 24rpx;
			border-top-left-radius: 24rpx;
			width: 100vw;
			height: 602rpx;
			overflow-y: auto;
			position: relative;
			.closeBtn {
				position: fixed;
				right: 34rpx;
				bottom: 538rpx;
				color: #C4C4C4;
			}
			.diaCont {
				position: absolute;
				top: 0;
				left: 0;
				right: 0;
				bottom: 0;
				padding: 40rpx 32rpx;
				.dialogInfo {
					position: relative;
					overflow-y: auto;
					.dialogTop {
						display: flex;
						justify-content: space-between;
						align-items: center;
						overflow-x: hidden;
						.diaImgArea{
							width: 180rpx;
							height: 180rpx;
							.dialogImg  {
								width: 100%;
								height: 100%;
								border-radius: 12rpx;
							}
						}
						.dialogRight {
							overflow: hidden;
							flex: 1;
							margin-left: 24rpx;
							padding-right: 84rpx;
							height: 180rpx;
							width: 100%;
							display: flex;
							flex-direction: column;
							justify-content: space-between;
							align-items: flex-start;
							.diaShopTitle {
								position: relative;
								width: 100%;
								margin-right: 84rpx;
								white-space: nowrap;
								text-overflow: ellipsis;
								overflow: hidden;
								font-size: 28rpx;
								color: #222222;
							}
							.diaShopCost {
								font-size: 44rpx;
								color: #EC3E55;
							}
							.diaShopSave {
								font-size: 28rpx;
								color: #69707C;
							}
						}
					}
					.cartColor {
						position: relative;
						width: 100%;
						margin-top: 40rpx;
						.colorTitle {
							font-size: 28rpx;
							color: #222222;
							text-align: left;
							margin-bottom: 16rpx;
						}
						.colorType {
							width: 100%;
							display: flex;
							justify-content: flex-start;
							align-items: center;
							flex-wrap: wrap;
							.colorItem {
								font-size: 28rpx;
								color: #222222;
								background-color: transparent;
								width: 132rpx;
								height: 64rpx;
								line-height: 64rpx;
								text-align: center;
								border: 1px solid #DDDDDD;
								border-radius: 8rpx;
								margin-right: 20rpx;
								margin-bottom: 10rpx;
							}
							.activeColor {
								background-color: #2A77FF;
								color: #FFFFFF;
							}
						}
					}
					.cartCount {
						position: relative;
						width: 100%;
						margin-top: 40rpx;
						margin-bottom: 50rpx;
						.countTitle {
							font-size: 28rpx;
							color: #222222;
							text-align: left;
							margin-bottom: 16rpx;
						}
						.inputCount {
							display: flex;
							justify-content: flex-start;
							align-items: center;
							.countRem, .countAdd {
								width: 80rpx;
								height: 64rpx;
								color: #838A93;
								border-top: 1px solid #838A93;
								border-bottom: 1px solid #838A93;
								text-align: center;
								line-height: 64rpx;
							}
							.countNum {
								width: 132rpx;
								height: 68rpx;
								border: 1px solid #838A93;
							}
							.countRem {
								border-left: 1px solid #838A93;
								border-top-left-radius: 8rpx;
								border-bottom-left-radius: 8rpx;
							}
							.countAdd {
								border-right: 1px solid #838A93;
								border-top-right-radius: 8rpx;
								border-bottom-right-radius: 8rpx;
							}
							.lastCount {
								opacity: 0.3;
							}
						}
					}
				}
			}
		}
	}
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
			padding-bottom: 40rpx;
			.shopImg {
				width: 100vw;
				height: 750rpx;
				image {
					width: 100%;
					height: 100%;
				}
			}
			.topDetail {
				padding: 36rpx 32rpx 40rpx 32rpx;
				background-color: #22282F;
				margin-bottom: 20rpx;
				.topTitle, .topInfo {
					// 超过两行自动省略号
					overflow: hidden;
					text-overflow:ellipsis;
					display:-webkit-box; 
					-webkit-box-orient:vertical;
					-webkit-line-clamp:2; 
					
				}
				.topTitle {
					font-size: 36rpx;
					color: #FFFFFF;
				}
				.topInfo {
					margin-top: 12rpx;
					font-size: 28rpx;
					color: #69707C;
				}
				.topMoney {
					display: block;
					font-size: 44rpx;
					color: #EC3E55;
					margin-top: 28rpx;
				}
				.topPreInfo {
					margin-top: 20rpx;
					display: flex;
					justify-content: space-between;
					align-items: center;
					text{
						font-size: 24rpx;
						color: #69707C;
					}
				}
			}
			.email {
				text-align: right;
				font-size: 28rpx;
				color: #FFFFFF;
			}
			.shopCartInfo {
				width: 100%;
				margin-top: 20rpx;
				padding: 40rpx 32rpx;
				background-color: #22282F;
				.cartInfo {
					font-size: 30rpx;
					color: #FFFFFF;
				}
				.cartInfoArea {
					margin-top: 40rpx;
					position: relative;
					width: 100%;
					height: 1836rpx;
					background-color: #575A60;
				}
			}
			.shopWillLike {
				background-color: #191E24;
				padding: 40rpx 32rpx;
				.cartLikeInfo {
					font-size: 30rpx;
					color: #FFFFFF;
				}
				.cartLikeList {
					margin: 20rpx 0;
					position: relative;
					width: 100%;
					display: flex;
					justify-content: space-between;
					align-items: center;
					flex-wrap: wrap;
					.midTitle {
						// 超过两行自动省略号
						overflow: hidden;
						text-overflow:ellipsis;
						display:-webkit-box; 
						-webkit-box-orient:vertical;
						-webkit-line-clamp:2; 
						font-size: 26rpx;
						color: #FFFFFF;
					}
					.btmTwoTitle {
						font-size: 32rpx;
						color: #EC3E55;
					}
					.btmTwoPreTitle {
						font-size: 28rpx;
						text-decoration: line-through;
						color: #69707C;
					}
				}
			}
		}
	}
</style>
