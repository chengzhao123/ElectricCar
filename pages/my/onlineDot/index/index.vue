
<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="服务网点" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
			<view slot="right">
				<image class="dot" src="/static/images/icons/my/dot_loc.png" mode=""></image>
			</view>
		</car-nav-bar>
		<!-- 顶部输入框 -->
		<view class="topInput">
			<view class="inputArea">
				<text class="search cuIcon cuIcon-search"></text>
				<input class="inputKuang" type="text" placeholder="请输入网点名称" />
			</view>
		</view>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				
				<car-map-cell v-for="(item, index) in 10" :key="index" margin_b10  @goMap="goMap"></car-map-cell>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'OnlineDotIndex',
		data() {
			return {
				
			}
		},
		computed: {
			Style() {
				let style = {
					'height': "calc(100vh  - 144rpx - " + this.CustomBar * 2 + 'rpx' + ")"
				}
				return style
			},
		},
		methods: {
			back() {
				uni.navigateBack()
			},
			goMap() {
				uni.navigateTo({
					url: '/pages/my/onlineDot/mapIndex/index'
				})
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
		.dot {
			width: 44rpx;
			height: 44rpx;
		}
		.topInput {
			background-color: #22282F;
			height: 144rpx;
			.inputArea {
				background-color: #313840;
				margin: 0 32rpx;
				height: 88rpx;
				border-radius: 12rpx;
				display: flex;
				justify-content: space-between;
				align-items: center;
				padding: 0 24rpx;
			
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
		}
		.content {
			width: 100%;
			height: 100%;
			padding-bottom: 20rpx;
			margin-top: 34rpx;
		}
	}
</style>
