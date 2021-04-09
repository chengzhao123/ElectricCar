<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="我的收藏" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-tab-bar :carTabStyle="TabItemStyle" :tabList="listArray" :tabIndex="currentIndex" @tabItemClick="changeIndex"></car-tab-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<view v-if="currentIndex == 0">
					<car-list-cell v-for="(item, index) in 10" :key='index' cellImg="/static/images/icons/mall/shopName.jpg">
						<view slot="topInfo">
							<text class="topTitle">本期话题：你觉得那哪个配件是你爱车上的“点睛之笔”</text>
						</view>
						<view slot="btmInfo">
							<text class="btmIndexTitle">03-05 21:22</text>
						</view>
					</car-list-cell>
				</view>
				<view v-if="currentIndex == 1" class="twoItem">
					<car-list-shop-cell v-for="(item, index) in 5" :key='index' shopImg="/static/images/icons/mall/shopName.jpg">
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
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'CollectIndex',
		data() {
			return {
				listArray:[ "动态", "收藏"],
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
			// TabbarStyle() {
			// 	let style = {
			// 		'background-color': '#22282F',
			// 		'color': '#FFFFFF',
			// 		'text-align': 'center',
			// 		'height': '88rpx',
			// 		'line-height': '88rpx',
			// 	}
			// 	return style
			// }
		},
		methods: {
			back() {
				uni.navigateBack()
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
		bottom: 0;
		left: 0;
		background-color: #191E24;
		.content {
			width: 100%;
			height: 100%;
			padding-bottom: 20rpx;
			.twoItem {
				width: 100%;
				padding:0 32rpx;
				margin-top: 20rpx;
				display: flex;
				justify-content: space-between;
				align-items: center;
				flex-wrap: wrap;
			}
			.topTitle {
				// 超过两行自动省略号
				overflow: hidden;
				text-overflow:ellipsis;
				display:-webkit-box; 
				-webkit-box-orient:vertical;
				-webkit-line-clamp:2; 
				font-size: 28rpx;
				color: #FFFFFF;
			}
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
			.btmIndexTitle {
				font-size: 28rpx;
				color: #69707C;
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
</style>
