<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" backColor="transparent">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style" @refresh="onRefresh" :triggered="triggered" refresher>
			<view class="content">
				<view class="bgImg">
					<image src="/static/images/icons/my/logo.png" mode="scaleToFill"></image>
					<view class="bgInfo">
						<text class="bgicon cuIcon cuIcon-info"></text>
						<text class="type">待付款</text>
					</view>
				</view>
				<view class="topArea">
					<view class="info">
						<text class="location cuIcon cuIcon-location"></text><text class="name">大黄鸭</text><text class="phone">159****3344</text>
					</view>
					<view class="area">
						<text class="pos">地址：</text><text class="areaName">四川省成都市锦江区三圣乡花卉市场</text>
					</view>
				</view>
				<car-list-cell class="item" :cellListStyle="cellListStyle">
					<view slot="topInfo">
						<text class="topTitle">上班出行顶配电摩NQi顶配上班出行顶配电摩NQi顶配上班出行顶配电摩NQi顶配上班出行顶配电摩NQi顶配…</text>
					</view>
					<view slot="btmInfo">
						<text class="btmIndexTitle">￥ 5699.00</text>
					</view>
					<view slot="btmRight">
						<view class="btmRight">
							<text class="list">订单编号：34567345676567<text class="copy">复制</text></text>
							<text class="list">下单时间：2021-02-25 22:02:11</text>
							<text class="list">支付方式：-</text>
							<text class="list">支付时间：-</text>
						</view>
					</view>
				</car-list-cell>
				<view class="btmLast">
					<view class="shopAll">
						<text class="shopM">商品价格</text>
						<text class="shopMNum">￥220.00</text>
					</view>
					<view class="extraAll">
						<text class="extraAllM">运费</text>
						<text class="extraAllMNum">￥12.00</text>
					</view>
					<view class="shopF">
						<text class="shopFTitle">应付款<text class="shopFNum">￥232.00</text></text>
					</view>
				</view>
				<view class="btnArea">
					<text class="delBtn">删除订单</text>
					<text class="payBtn">去支付</text>
				</view>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'OrderDetail',
		data(){
			return {
				triggered: false
			}
		},
		onLoad() {
			
		},
		computed: {
			Style() {
				let style = {
					// #ifdef APP-PLUS || H5
					'height': "calc(100vh  - " + this.CustomBar * 2 + 'rpx' + ")"
					// #endif
					// #ifdef MP-WEIXIN
					'height': "calc(100vh - 100rpx - " + this.CustomBar * 2 + 'rpx' + ")"
					// #endif
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
			},
			initData() {
				setTimeout(() => {
					this._refreshing = false
					this.triggered = false
				}, 1000)
			
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
			display: block;
			z-index: 2;
			overflow: hidden;
			.bgImg {
				width: 100%;
				height: 292rpx;
				position: relative;
				z-index: 1;
				image {
					width: 100%;
					height: 100%;
				}
				.bgInfo {
					width: 100%;
					height: 50rpx;
					position: absolute;
					top: 50%;
					left: 50%;
					margin-left: -50%;
					margin-top: -25rpx;
					z-index: 3;
					display: flex;
					justify-content: center;
					align-items: center;
					font-size: 36rpx;
					color: #FFFFFF;
					.bgicon {
						margin-right: 15rpx;
					}
				}
			}
			.topArea {
				background-color: #22282F;
				position: relative;
				z-index: 4;
				background-color: #22282F;
				padding: 40rpx 32rpx;
				border-top-right-radius: 24rpx;
				border-top-left-radius: 24rpx;
				margin-top: -32rpx;
				.info {
					font-size: 26rpx;
					color: #FFFFFF;
					margin-bottom: 8rpx;
					.location {
						margin-right: 16rpx;
					}
					.name {
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
			.item {
				background-color: #22282F;
				.topTitle {
					// 超过两行自动省略号
					overflow: hidden;
					text-overflow:ellipsis;
					display:-webkit-box; 
					-webkit-box-orient:vertical;
					-webkit-line-clamp:2; 
					font-size: 32rpx;
					color: #FFFFFF;
				},
				.btmIndexTitle {
					font-size: 32rpx;
					color: #FFFFFF;
				}
				.btmRight {
					margin-top: 32rpx;
					border-top: 1px solid #2E343C;
					
					display: flex;
					flex-direction: column;
					justify-content: space-between;
					align-items: flex-start;
					.list {
						font-size: 26rpx;
						color: #FFFFFF;
						margin-top: 30rpx;
						.copy {
							margin-left: 26rpx;
							background-color: #69707C;
							border-radius: 32rpx;
							padding: 4rpx 10rpx;
							font-size: 22rpx;
						}
					}
				}
			}
			.btmLast {
				padding: 40rpx 32rpx;
				background-color: #22282F;
				font-size: 26rpx;
				color: #FFFFFF;
				margin-bottom: 20rpx;
				.shopAll, .extraAll {
					display: flex;
					justify-content: space-between;
					align-items: center;
					margin-bottom: 30rpx;
				}
				.shopF {
					display: flex;
					justify-content: flex-end;
					align-items: center;
					.shopFNum {
						font-size: 32rpx;
						margin-left: 20rpx;
					}
				}
			}
			.btnArea {
				padding: 12rpx 32rpx;
				background-color: #22282F;
				font-size: 28rpx;
				color: #838A93;
				display: flex;
				justify-content: flex-end;
				align-items: center;
				.payBtn {
					color: #EC3E55;
					margin-left: 32rpx;
					border: 1px solid #EC3E55;
				}
				.payBtn, .delBtn {
					padding: 18rpx 32rpx;
					border-radius: 44rpx;
				}
				.delBtn {
					border: 1px solid #838A93;
				}
			}
		}
	}
</style>
