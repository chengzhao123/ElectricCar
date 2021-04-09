<template>
	<view class="car-map-cell" :class="margin_b10 ? 'margin_b10' : '' " @click="goMap">
		<view class="car-map-cage" :style="[mapCellStyle]">
			<view class="car-map-img">
				<image :src="MapPosImg" mode="scaleToFill"></image>
			</view>
			<view class="car-map-right">
				<view class="car-map-dis">
					<text class="car-pos">成都市修车行</text>
					<text class="car-detail-pos">成都市武侯区武侯大道122号成都市武侯区武侯大道122号成都市武侯区武侯大道122号</text>
				</view>
				<view class="car-map-r">
					<view class="car-map-r-l">
						
					</view>
					<view class="car-map-r-r">
						<image class="loc" src="/static/images/icons/my/loc.png" mode="widthFix"></image>
						<text class="car-distance">4.4km</text>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'car-map-cell',
		props: {
			MapPosImg: {
				type: String,
				default: '/static/images/icons/mall/shopName.jpg'
			},
			margin_b10: {
				type: Boolean,
				default: false
			},
			mapCellStyle: {
				type: Object,
				default: function() {
					return {}
				}
			}
		},
		data() {
			return {
				
			}
		},
		methods: {
			goMap() {
				this.$emit('goMap')
			}
		}
	}
</script>

<style lang="scss" scoped>
	.margin_b10 {
		margin-bottom: 20rpx;
	}
	.car-map-cell {
		height: 180rpx;
		.car-map-cage {
			margin: 0 32rpx;
			padding: 20rpx 22rpx;
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
			border-radius: 12rpx;
			background-color: #22282F;
			box-shadow: 0px 2px 8px 0px rgba(0, 0, 0, 0.20);
			overflow: hidden;
			position: relative;
			.car-map-img {
				width: 136rpx;
				height: 136rpx;
				margin-right: 24rpx;
				image {
					width: 100%;
					height: 100%;
				}
			}
			.car-map-right {
				flex: 1;
				height: 100%;
				display: flex;
				flex-direction: row;
				justify-content: space-between;
				align-items: center;
				.car-map-dis {
					margin-right: 80rpx;
					flex: 1;
					width: 0;
					height: 100%;
					display: flex;
					flex-direction: row;
					align-items: center;
					.car-pos {
						position: absolute;
						top: 20rpx;
						color: #FFFFFF;
						font-size: 30rpx;
					}

					.car-detail-pos {
						position: relative;
						overflow: hidden;
						white-space: nowrap;
						text-overflow: ellipsis;
						margin-top: 8rpx;
						color: #69707C;
						font-size: 24rpx;
					}
				}
				.car-map-r {
					display: flex;
					flex-direction: row;
					justify-content: space-between;
					align-items: center;
					.car-map-r-l {
						width: 1px;
						height: 136rpx;
						display: block;
						background-color: #343B43;
					}
					.car-map-r-r {
						padding-left: 26rpx;
						display: flex;
						flex-direction: row;
						flex-direction: column;
						justify-content: center;
						align-items: center;
						.loc {
							width: 34rpx;
						}
						.car-distance {
							margin-top: 8rpx;
							color: #FFFFFF;
							font-size: 24rpx;
						}
					}
				}
				

			}
		}

	}
</style>
