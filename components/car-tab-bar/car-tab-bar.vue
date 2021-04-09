<template>
	<view class="car-tabbar" :style="[contentStyle]">
		<scroll-view scroll-x scroll-with-animation>
			<view class="car-tabbar-list" :class="justPos">
				<view v-for="(item, index) in tabList" :key="index" class="car-tabbar-item"
					:style="[carTabStyle]"
					:class="index == tabIndex ? 'car-tabbar-active': '' "
					@click="cartabbarClick(index)">
					<view class="car-tabbar-name">{{item}}</view>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		name: 'CarTabBar',
		data() {
			return {

			}
		},
		props: {
			contentStyle: {
				type: Object,
				default: function() {
					return {
						'background-color': '#22282F',
						'color': '#FFFFFF',
						'text-align': 'center',
						'height': '88rpx',
						'line-height': '88rpx'
					}
				}
			},
			carTabStyle: {
				type: Object,
				default: function() {
					return {}
				}
			},
			tabList: {
				type: Array,
				default: []
			},
			tabIndex: {
				type: Number,
				default: 0
			},
			justPos: {
				type: String,
				default : 'justify-center' //  justify-center  justify-end justify-start
			}
		},
		methods: {
			cartabbarClick(e) {
				this.$emit('tabItemClick', e)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.car-tabbar {
		box-sizing: border-box;
		.car-tabbar-list {
			width: 100%;
			display: flex;
			align-items: center;
			box-sizing: border-box;
			white-space: nowrap;
			.car-tabbar-item {
				font-size: 32rpx;
				position: relative;
				color: #838A93;
				.car-tabbar-name {
					padding: 0 32rpx;
				}
			}
			.car-tabbar-active {
				font-size: 36rpx;
				color: #FFFFFF;
				font-weight: bolder;
			}
			
			.car-tabbar-active::before {
				content: '';
				position: absolute;
				width: 28rpx;
				height: 4rpx;
				left: 50%;
				margin-left: -14rpx;
				bottom: 2rpx;
				background-color: #2A77FF;
			}
		}
	}
</style>
