<template>
	<view class="mf">
		<car-nav-bar isBack title="商城" backColor="#191E24">
			<view slot="right">
				<view @click="goCartCar">
					<view class="cart">
						<image src="/static/images/icons/mall/cartCar.png" mode="scaleToFill"></image>
					</view>
					<text class="shopNum">7</text>
				</view>
			</view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style" @refresh="onRefresh" :triggered="triggered" isCanRefresher>
			<view class="content">
				<!-- 顶部输入框 -->
				<view class="inputArea">
					<text class="search cuIcon cuIcon-search"></text>
					<input class="inputKuang" type="text" placeholder="搜索商品" />
				</view>
				<!-- 轮播图 -->
				<view class="lunbo">
					<swiper class="swiper" indicator-dots autoplay :interval="2000" circular
						indicator-active-color="#FFFFFF" indicator-color="rgba(255,255,255,0.3)">
						<swiper-item>
							<view class="swiper-item">
								<image class="swimg" src="/static/images/icons/mall/lunbo.jpg" mode="scaleToFill">
								</image>
							</view>
						</swiper-item>
						<swiper-item>
							<view class="swiper-item">
								<image class="swimg" src="/static/images/icons/mall/lunbo.jpg" mode="scaleToFill">
								</image>
							</view>
						</swiper-item>
						<swiper-item>
							<view class="swiper-item ">
								<image class="swimg" src="/static/images/icons/mall/lunbo.jpg" mode="scaleToFill">
								</image>
							</view>
						</swiper-item>
					</swiper>
				</view>
				<!-- tab切换栏 -->
				<car-tab-bar justPos="justify-start" :carTabStyle="carTabStyle" :contentStyle="tabbarStyle"
					:tabList="listArray" :tabIndex="currentIndex" @tabItemClick="changeIndex" />
				<!-- 商品列表 -->
				<view class="shopList">
					<car-list-shop-cell v-for="(item, index) in 5" :key='index' @shopItemIndex="shopIndex(item, index)"
						shopImg="/static/images/icons/mall/shopName.jpg">
						<view slot="midTitle">
							<text
								class="midTitle">上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行上班出行
								顶配电摩 NQi顶配版理论续航800km</text>
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
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'Mall',
		data() {
			return {
				triggered: false,
				listArray: ["推荐", "全部整车", "后靠背", "冬季保暖", "骑行"],
				currentIndex: 0
			};
		},
		onLoad() {

		},
		computed: {
			Style() {
				let style = {
					// #ifdef APP-PLUS || MP-WEIXIN
					'height': "calc(100vh - " + this.CustomBar * 2 + 'rpx' + ")"
					// #endif
					// #ifdef H5
					'height': "calc(100vh - 100rpx - " + this.CustomBar * 2 + 'rpx' + ")"
					// #endif
				}
				return style
			},
			tabbarStyle() {
				let style = {
					'background-color': '#191E24',
					'color': '#FFFFFF',
					'text-align': 'center',
					'height': '88rpx',
					'line-height': '88rpx',
					'background-color': '#191E24',
					'padding-bottom': '12rpx'
				}
				return style
			},
			carTabStyle() {
				let style = {
					'padding-bottom': '12rpx'
				}
				return style
			}
		},
		methods: {
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
			shopIndex() {
				uni.navigateTo({
					url: '/pages/mall/shopIndex/index'
				})
			},
			goCartCar() {
				uni.navigateTo({
					url: '/pages/mall/cartCar/index'
				})
			},
			onRefresh() {
				if (this._refreshing) return
				this._refreshing = true;
				this.triggered = true;
				this.initData();
			},
			changeIndex(e) {
				console.log(e)
				this.currentIndex = e
			}
		}
	}
</script>

<style lang="scss" scoped>
	.mf {
		position: absolute;
		top: 0;
		right: 0;
		left: 0;
		bottom: 0;
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

			// padding-top: 20rpx;
			.inputArea {
				background-color: #313840;
				margin: 0 32rpx;
				height: 88rpx;
				border-radius: 12rpx;
				display: flex;
				justify-content: space-between;
				align-items: center;
				padding: 28rpx 24rpx;

				.search {
					font-size: 32rpx;
					color: #69707C;
				}

				.inputKuang {
					margin-left: 18rpx;
					font-size: 28rpx;
					flex: 1;
					height: 100%;
					line-height: 88rpx;
					color: #FFFFFF;
				}

				.inputKuang::-webkit-input-placeholder {
					color: #69707C
				}
			}

			.lunbo {
				position: relative;
				padding: 0 32rpx;
				margin: 40rpx 0 20rpx 0;
				height: 310rpx;
				width: 100%;

				.swiper,
				.swiper-item,
				.swimg {
					width: 100%;
					height: 100%;
				}

				.swimg {
					border-radius: 12rpx;
				}
			}

			.shopList {
				position: relative;
				padding: 0 32rpx;
				margin-top: 48rpx;
				width: 100%;
				display: flex;
				justify-content: space-between;
				align-items: center;
				flex-wrap: wrap;

				.midTitle {
					// 超过两行自动省略号
					overflow: hidden;
					text-overflow: ellipsis;
					display: -webkit-box;
					-webkit-box-orient: vertical;
					-webkit-line-clamp: 2;
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
</style>
