<template>
	<view class="car-navbar" :style="[navStyle]">
		<!-- 左中右 三个-->
		<block v-if="isBack">
			<view class="car-navbar-leftContent">
				<view class="car-navbar-left" @click="back">
					<slot name="left"></slot>
				</view>
				<view class="car-navbar-center">
					<text>{{title}}</text>
				</view>
				<view class="car-navbar-right">
					<slot name="right"></slot>
				</view>
			</view>
		</block>
		<!-- 搜索框 -->
		<!-- <block v-if="isSearch">
			<input type="text" value="" />
		</block> -->
	</view>
</template>

<script>
	export default {
		name: "car-nav-bar",
		data() {
			return {

			};
		},
		props: {
			isSearch: {
				type: Boolean,
				default: false
			},
			isBack: {
				type: Boolean,
				default: false
			},
			isRight: {
				type: Boolean,
				default: false
			},
			title: {
				type: String,
				default: ''
			},
			backColor: {
				type:String,
				default: '#191E24'
			},
			leftColor: {
				type:String,
				default: '#FFFFFF'
			},
		},
		computed: {
			navStyle() {
				let style = {
					'background-color': this.backColor,
					'padding-top': this.StatusBar * 2 + 'rpx',
					'height': this.CustomBar * 2 + 'rpx'
				}
				return style
			}
		},
		methods: {
			back() {
				this.$emit('back')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.car-navbar {
		// height: 100rpx;
		display: flex;
		z-index: 999;
		justify-content: space-between;
		align-items: center;
		font-size: 36rpx;
		.car-navbar-leftContent {
			width: 100%;
			display: flex;
			justify-content: space-between;
			align-items: center;
			.car-navbar-left,.car-navbar-right,.car-navbar-center {
				z-index: 999;
				color: #FFFFFF;
				display: flex;
				justify-content: center;
				align-items: center;
				position: relative;
			}
			.car-navbar-left {
				min-width: 36rpx;
				margin-left: 32rpx;
			}
			.car-navbar-center {
				font-size: 36rpx;
				font-weight: bolder;
			}
			.car-navbar-right {
				min-width: 36rpx;
				font-size: 32rpx;
				margin-right: 32rpx;
			}
		}
	}
</style>
