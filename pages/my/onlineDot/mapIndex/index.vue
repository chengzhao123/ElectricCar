<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="服务网点" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
			<view slot="right">
				<image class="dot" src="/static/images/icons/my/dot_loc.png" mode=""></image>
			</view>
		</car-nav-bar>

		<car-container :contentStyle="Style">
			<view class="content">
				<map class="maps" :style="[Style]" :latitude="latitude" :longitude="longitude" :markers="covers"></map>
				<!-- 顶部输入框 -->
				<!-- #ifndef APP-PLUS -->
				<view class="topInput">
					<view class="inputArea">
						<image class="sear" src="/static/images/icons/my/search.png" mode=""></image>
						<input class="inputKuang" type="text" placeholder="请输入网点名称" v-model="search" />
						<image class="closea" src="/static/images/icons/my/del.png" mode=""></image>
					</view>
				</view>
				<view v-if="search.length > 0" class="blurSearchList" :style="[SearchList]">
					<car-map-cell v-for="(item, index) in 10" :key="index" :mapCellStyle="mapCellStyle"></car-map-cell>
				</view>
				<view class="nowPos">
					<car-map-cell id="searchList"></car-map-cell>
				</view>
				<view class="searchBtn" @click="surePos">
					<image class="surepos" src="/static/images/icons/my/loc.png" mode=""></image>
				</view>
				<!-- #endif -->
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'MapIndex',
		data() {
			return {
				canClick: true,
				search: '',
				title: 'map',
				latitude: 39.909,
				longitude: 116.39742,
				covers: [{
					id: 0, // 使用 marker点击事件 需要填写id
					latitude: 39.909,
					longitude: 116.39742,
					iconPath: '/static/images/icons/my/location.png',
					width: 32,
					height: 32,

				}]
			}
		},
		computed: {
			Style() {
				let style = {
					'height': "calc(100vh - " + this.CustomBar * 2 + 'rpx' + ")"
				}
				return style
			},
			mapCellStyle() {
				let style = {
					'border-bottom': '1px solid #343B43',
					'margin': 0
				}
				return style
			},
			SearchList() {
				let style = {
					'top': 150 + this.CustomBar * 2 + 'rpx'
				}
				return style
			}
		},
		mounted() {
			// #ifdef APP-PLUS
			const m = uni.getSubNVueById("maps")
			m.show()
			m.setStyle({
				height: this.WindowHeight - this.CustomBar - 6 + 'px',
				top: this.CustomBar + 6 + 'px',
				width: '100%'
			})
			uni.$on('getLocation', (res) => {
				let r = res.data
				this.longitude = r.longitude;
				this.latitude = r.latitude;
				this.covers[0].longitude = r.longitude;
				this.covers[0].latitude = r.latitude;
			})
			// #endif

			// #ifndef APP-PLUS
			this.getLoc()
			// #endif
		},
		methods: {
			getLoc() {
				console.log('这是父页面')
				uni.getLocation({
					// #ifndef MP-WEIXIN
					type: 'wgs84',
					// #endif
					// #ifdef MP-WEIXIN
					type: 'gcj02',
					// #endif
					success: (res) => {
						console.log(res)
						this.longitude = res.longitude;
						this.latitude = res.latitude;
						this.covers[0].longitude = res.longitude;
						this.covers[0].latitude = res.latitude;
						setTimeout(() => {
							this.canClick = true
						}, 1000)
					},
					fail: (err) => {
						console.log(err)
					}
				});
			},
			back() {
				uni.navigateBack()
			},
			surePos() {
				if (!this.canClick) return
				this.canClick = false
				this.getLoc()
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

		// background-color: #191E24;
		.dot {
			width: 44rpx;
			height: 44rpx;
		}

		.content {
			width: 100%;
			height: 100%;
			position: relative;

			.topInput {
				position: absolute;
				top: 20rpx;
				left: 0;
				right: 0;

				.inputArea {
					background-color: #313840;
					margin: 0 32rpx;
					height: 88rpx;
					border-radius: 12rpx;
					display: flex;
					justify-content: space-between;
					align-items: center;
					padding: 28rpx 24rpx;

					.sear {
						width: 32rpx;
						height: 32rpx;
					}

					.inputKuang {
						margin-left: 18rpx;
						font-size: 28rpx;
						flex: 1;
						height: 100%;
						line-height: 88rpx;
						z-index: 9999;
						color: #FFFFFF;
					}

					.inputKuang::-webkit-input-placeholder {
						color: #69707C
					}

					.closea {
						margin-left: 32rpx;
						width: 32rpx;
						height: 32rpx;
					}
				}
			}

			.maps {
				position: relative;
				width: 100%;
			}

			.nowPos {
				position: fixed;
				left: 0;
				right: 0;
				bottom: 32rpx;
				z-index: 9999;
			}

			.blurSearchList {
				position: fixed;
				border-radius: 12rpx;
				height: 360rpx;
				left: 32rpx;
				right: 32rpx;
				overflow: scroll;
				background-color: #22282F;
				z-index: 9999;
			}

			.searchBtn {
				position: fixed;
				right: 32rpx;
				bottom: 240rpx;
				text-align: center;
				display: flex;
				align-items: center;
				justify-content: center;
				font-size: 40rpx;
				width: 88rpx;
				height: 88rpx;
				background-color: #FFFFFF;
				border-radius: 50%;
				z-index: 9999;

				.surepos {
					width: 44rpx;
					height: 44rpx;
				}
			}
		}
	}
</style>
