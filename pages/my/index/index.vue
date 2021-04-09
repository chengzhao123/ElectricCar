<template>
	<view class="mf">
		<car-nav-bar isBack title="我的" backColor="#191E24">
			<view slot="right">
				<view class="cart" @click="goSet">
					<image src="/static/images/icons/my/set.png" mode="scaleToFill"></image>
				</view>
			</view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style" @refresh="onRefresh" :triggered="triggered" isCanRefresher>
			<view class="content">
				<view class="header">
					<view class="headerImg" @click="goMineInfo">
						<image src="/static/images/icons/my/userImg.png" mode="widthFix"></image>
					</view>
					<view class="rightHeader">
						<view class="loginStatus">{{isLogin ? '纳米纳米纳米无敌' : '未登录' }}</view>
						<view v-if="!isLogin" class="loginClick">点击登录</view>
						<view v-else class="isLoginClick" @click="goScoreDetail">
							<view class="scoreL">
								<image class="scoreIc" src="/static/images/icons/my/score.png" mode="scaleToFill"></image>
								<view class="scoreArea">
									<text class="scoreT">积分</text>
									<text class="scoreB">{{score}}</text>
								</view>
							</view>
							<view class="scoreR">
								<text class="cuIcon cuIcon-right"></text>
							</view>
						</view>
					</view>
					<view class="rightBack">
						<image src="/static/images/icons/my/myTopBack.png" mode="heightFix"></image>
					</view>
				</view>
				<view v-if="isLogin" class="loginInfo">
					<view class="item" @click="goOrder">
						<image src="/static/images/icons/my/whitePay.png" mode="widthFix"></image>
						<view class="items">待付款</view>
					</view>
					<view class="item" @click="goOrder">
						<image src="/static/images/icons/my/whiteGet.png" mode="widthFix"></image>
						<view class="items">待收货</view>
					</view>
					<view class="item" @click="goOrder">
						<image src="/static/images/icons/my/allOrder.png" mode="widthFix"></image>
						<view class="items">全部订单</view>
					</view>
					<view class="item" @click="goMyCollect">
						<image src="/static/images/icons/my/myLove.png" mode="widthFix"></image>
						<view class="items">我的收藏</view>
					</view>
				</view>
				<view class="service">
					<view class="hTitle">我的服务</view>
					<view class="info">
						<view class="item" @click="goOnlineXiu">
							<image src="/static/images/icons/my/onlineXiu.png" mode="widthFix"></image>
							<view class="items">在线报修</view>
						</view>
						<view class="item" @click="goChat">
							<image src="/static/images/icons/my/onlinePeople.png" mode="widthFix"></image>
							<view class="items">在线客服</view>
						</view>
						<view class="item" @click="goServeiceOnlineDot">
							<image src="/static/images/icons/my/servicePos.png" mode="widthFix"></image>
							<view class="items">服务网点</view>
						</view>
						<view class="item">
							<image src="/static/images/icons/my/lostSay.png" mode="widthFix"></image>
							<view class="items">失窃上报</view>
						</view>
					</view>
				</view>
				<view v-if="isLogin" class="media lo">
					<view class="hTitle">
						<text class="mediaTitle">我的设备</text>
						<text class="removeBind">解除绑定<text class="cuIcon cuIcon-right"></text></text>
					</view>
					<view class="infos">
						<view class="infoOne">
							<text class="dist">10KM</text>
							<view class="emp">
								<view class="all">
									<view class="now"></view>
								</view>
							</view>
							<text class="em">20%</text>
						</view>
					</view>
					<image class="mediaImg" src="/static/images/icons/my/car.png" mode="scaleToFill"></image>
				</view>
				<view v-else class="media">
					<view class="hTitle">我的设备</view>
					<view class="info">
						<view class="btn cu-btn block radius" @click="goBindMedia">
							<text class="cuIcon cuIcon-add"></text><text class="bind">绑定设备</text>
						</view>
					</view>
				</view>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'MyIndex',
		data() {
			return {
				isLogin: true,
				triggered: false,
				score: 10000000
			};
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
		},
		methods: {
			goOrder() {
				uni.navigateTo({
					url: '/pages/my/order/index/index'
				})
			},
			goChat() {
				uni.navigateTo({
					url: '/pages/my/chat/index/index'
				})
			},
			goScoreDetail() {
				uni.navigateTo({
					url: '/pages/my/score/index'
				})
			},
			goServeiceOnlineDot() {
				uni.navigateTo({
					url: '/pages/my/onlineDot/index/index'
				})
			},
			goSet() {
				uni.navigateTo({
					url: '/pages/my/set/index/index'
				})
			},
			goOnlineXiu() {
				uni.navigateTo({
					url: '/pages/my/baoxiu/index/index'
				})
			},
			goMyCollect() {
				uni.navigateTo({
					url: '/pages/my/collect/index/index'
				})
			},
			goMineInfo() {
				uni.navigateTo({
					url: '/pages/my/info/index/index'
				})
			},
			goBindMedia() {
				uni.navigateTo({
					url: '/pages/my/bindmedia/index/index'
				})
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
			onRefresh() {
				if (this._refreshing) return
				this._refreshing = true;
				this.triggered = true;
				this.initData();
			}
		}
	}
</script>

<style lang="scss">
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
		.content {
			position: relative;
			padding:0 32rpx;
			padding-bottom: 20rpx;
			width: 100%;
			height: 100%;
			.header {
				padding-top: 32rpx;
				display: flex;
				justify-content: flex-start;
				align-items: center;
				flex-wrap: nowrap;
				.headerImg {
					width: 120rpx;
					height: 120rpx;
					border-radius: 50%;
				}

				.rightHeader {
					margin-left: 32rpx;
					display: flex;
					flex-direction: column;
					justify-content: space-around;
					align-items: flex-start;
					height: 120rpx;
					width: 194rpx;
					position: relative;
					.loginStatus {
						width: 100%;
						text-overflow: ellipsis;
						white-space: nowrap;
						overflow: hidden;
						font-size: 36rpx;
						color: #FFFFFF;
						font-weight: bolder;
					}

					.loginClick {
						display: flex;
						justify-content: space-between;
						align-items: center;
						font-size: 26rpx;
						color: #69707C;
					}
					.isLoginClick {
						z-index: 100;
						display: flex;
						justify-content: space-between;
						align-items: flex-end;
						.scoreL {
							display: flex;
							justify-content: flex-start;
							align-items: center;
							white-space: nowrap;
							.scoreIc {
								width: 32rpx;
								height: 32rpx;
							}
							.scoreArea {
								font-size: 26rpx;
								color: #A0A7B3;
								.scoreT {
									margin: 0 12rpx 0 8rpx;
								}
								.scoreB {
									
								}
							}
						}
						.scoreR {
							text {
								font-size: 26rpx;
								color: #A0A7B3;
							}
						}
					}
				}
				.rightBack {
					height: 214rpx;
					image {
						width: 100%;
						height: 100%;
					}
				}
			}

			.loginInfo {
				padding: 40rpx 40rpx 60rpx 40rpx;
				margin-top: 100rpx;
				display: flex;
				justify-content: space-between;
				align-items: center;

				.item {
					text-align: center;

					image {
						width: 40rpx;
					}

					.items {
						font-size: 24rpx;
						margin-top: 22rpx;
						color: #FFFFFF;
					}
				}
			}
			.lo {
				height: 420rpx;
				background-image: url(/static/images/icons/my/mediaBack.png) !important;
				background-size: cover;
				.mediaImg {
					z-index: 10;
					position: absolute;
					right: 0;
					bottom: 40rpx;
					width: 402rpx;
					height: 260rpx;
				}
				.infos {
					z-index: 101;
					position: absolute;
					left: 40rpx;
					bottom: 80rpx;
					.infoOne {
						position: relative;
						.em {
							font-style: italic;
							font-size: 28rpx;
							color: #FFFFFF;
							margin-left: 14rpx;
						}
						.dist {
							color: #FFFFFF;
							font-size: 64rpx;
							font-style: italic;
							font-weight: bolder;
							display: block;
						}
						.emp {
							display: inline-block;
							border: 1px solid #C4C9CD;
							border-radius: 6rpx;
							width: 50rpx;
							height: 24rpx;
							padding: 2rpx;
							background-color: transparent;
							.all {
								width: 100%;
								height: 100%;
								position: relative;
								.now {
									width: 10rpx;
									background-color: #E14B42;
									height: 100%;
								}
							}
							.all::after {
								content: '';
								position: absolute;
								right: -10rpx;
								top: 4.5rpx;
								width: 2rpx;
								height: 8rpx;
								background-color: #C4C9CD;
							}
						}
					}
				}
			}
			.service,
			.media {
				padding: 40rpx 40rpx 60rpx 40rpx;
				margin-top: 32rpx;
				border: 1px solid #22282F;
				// background-color: #22282F;
				// border-radius: 12rpx;
				position: relative;
				
				
				.hTitle {
					display: flex;
					justify-content: space-between;
					align-items: center;
					font-size: 30rpx;
					color: #69707C;
					margin-bottom: 32rpx;

					.mediaTitle {
						font-size: 30rpx;
						color: #FFFFFF;
					}

					.removeBind {
						font-size: 26rpx;
						font-weight: lighter;
						color: #FFFFFF;
					}
				}
				.info {
					display: flex;
					justify-content: space-between;
					align-items: center;
					position: relative;
					.infoOne {
						position: relative;
					}
					
					.item {
						text-align: center;

						image {
							width: 40rpx;
						}

						.items {
							font-size: 24rpx;
							margin-top: 22rpx;
							color: #FFFFFF;
						}
					}

					.btn {
						width: 100%;
						font-weight: bold;
						height: 100rpx;
						background-color: #2A77FF;
						font-size: 32rpx;
						color: #FFFFFF;

						.bind {
							margin-left: 13rpx;
						}
					}
				}
			}
		}
	}
</style>
