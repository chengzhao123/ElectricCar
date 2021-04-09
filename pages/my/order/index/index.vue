<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="我的订单" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-tab-bar id="car-tabbar" :carTabStyle="TabItemStyle" :tabList="listArray" :tabIndex="currentIndex"
			@tabItemClick="changeIndex"></car-tab-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<car-list-cell v-for="(item, index) in 10" :key='index' class="item" :cellListStyle="cellListStyle" @itemClick="itemClick(index)" cellImg="/static/images/icons/mall/shopName.jpg">
					<view slot="topLR">
						<view class="topLR">
							<text class="type">待付款</text>
							<text class="time">05-11 12:22</text>
						</view>
					</view>
					<view slot="topInfo">
						<text class="topTitle">上班出行顶配电摩NQi顶配上班出行顶配电摩NQi顶配上班出行顶配电摩NQi顶配上班出行顶配电摩NQi顶配…</text>
					</view>
					<view slot="btmInfo">
						<text class="btmIndexTitle">￥ 5699.00</text>
					</view>
					<view slot="btmRight">
						<view class="btmRight">
							<text class="btnOne">取消订单</text>
							<text class="btnTwo">去支付</text>
						</view>
					</view>
				</car-list-cell>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'OrderIndex',
		data() {
			return {
				listArray: ["待付款","已付款","已完成","已取消"],
				currentIndex: 0
			}
		},
		computed: {
			Style() {
				let style = {
					'height': "calc(100vh - 88rpx - " + this.CustomBar * 2 + 'rpx' + ")"
				}
				return style
			},
			TabItemStyle() {
				let style = {
					'flex': 1
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
			itemClick(e){
				console.log(e)
				uni.navigateTo({
					url: '/pages/my/order/detail/index'
				})
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
		background-color: #191E24;
		.content {
			position: relative;
			width: 100%;
			height: 100%;
			.item {
				background-color: #22282F;
				.topLR {
					display: flex;
					justify-content: space-between;
					align-items: center;
					font-size: 28rpx;
					padding-bottom: 30rpx;
					margin-bottom: 32rpx;
					border-bottom: 1px solid #2E343C;
					.type {
						color:#EC3E55
					}
					.time {
						color: #69707C;
					}
				}
				.topTitle {
					// 超过两行自动省略号
					overflow: hidden;
					text-overflow:ellipsis;
					display:-webkit-box; 
					-webkit-box-orient:vertical;
					-webkit-line-clamp:2; 
					font-size: 32rpx;
					color: #FFFFFF;
				}
				.btmIndexTitle {
					font-size: 32rpx;
					color: #FFFFFF;
				}
				.btmRight {
					display: flex;
					justify-content: flex-end;
					align-content: center;
					margin-top: 40rpx;
					.btnOne, .btnTwo {
						font-size: 28rpx;
						padding: 18rpx 32rpx;
						border-width: 1px;
						border-style: solid;
						border-radius: 44rpx;
					}
					.btnOne {
						border-color: #838A93;
						color: #838A93;
					},
					.btnTwo {
						border-color: #EC3E55;
						color: #EC3E55;
						margin-left: 32rpx;
					}
				}
			}
			
		}
	}
</style>
