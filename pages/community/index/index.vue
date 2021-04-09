<template>
	<view class="mf">
		<car-nav-bar isBack title="图表" backColor="#22282F"></car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<canvas canvas-id="canvasColumn" id="canvasColumn" class="charts" @touchstart="touchstart"
					@touchmove="touchmove" @touchend="touchend" :style="[CStyle]" echartsH5 echartsApp />
			</view>
		</car-container>
	</view>
</template>

<script>
	import uCharts from '../../../js_sdk/u-charts/u-charts/u-charts.js';
	var _self;
	var canvaLineA = null;
	export default {
		data() {
			return {
				cWidth: '',
				cHeight: '',
				pixelRatio: 1
			}
		},
		onLoad() {
			_self = this;
			//#ifdef MP-ALIPAY
			uni.getSystemInfo({
				success: function(res) {
					if (res.pixelRatio > 1) {
						//正常这里给2就行，如果pixelRatio=3性能会降低一点
						//_self.pixelRatio =res.pixelRatio;
						_self.pixelRatio = 2;
					}
				}
			});
			//#endif
			this.cWidth = this.windowWidth;
			this.cHeight = uni.upx2px(800);
			this.getServerData()
		},
		computed: {
			Style() {
				let style = {
					// #ifdef APP-PLUS || H5
					'height': "calc(100vh - " + this.CustomBar * 2 + 'rpx' + ")"
					// #endif
					// #ifdef MP-WEIXIN
					'height': "calc(100vh - 100rpx - " + this.CustomBar * 2 + 'rpx' + ")"
					// #endif
				}
				return style
			},
			CStyle() {
				let style = {
					'width': this.windowWidth + 'px',
					'height': 800 + 'rpx',
					'background-color': '#191E24',
					'z-index': 1000
				}
				return style
			}
		},
		methods: {
			touchstart(e) {
				canvaLineA.scrollStart(e);
			},
			touchmove(e) {
				canvaLineA.scroll(e);
			},
			touchend(e) {
				canvaLineA.scrollEnd(e);
			},
			getServerData() {
				let Column = {
					categories: [],
					series: []
				};
				//这里我后台返回的是数组，所以用等于，如果您后台返回的是单条数据，需要push进去
				Column.categories = ['0', '10', '20', '30', '40', '50', '60', '70', '80', '90', '100']
				//这里的series数据是后台做好的，如果您的数据没有和前面我注释掉的格式一样，请自行拼接数据
				Column.series = [
					{data: [55, 20, 25, 37, 41, 20, 25, 37, 42, 20, 25]},
					{data: [22, 40, 55, 17, 71, 20, 75, 87, 22, 50, 35]}
					
				];
				_self.showColumn("canvasColumn", Column);
			},
			showColumn(name, data) {
				canvaLineA = new uCharts({
					$this: _self,
					canvasId: name,
					type: 'area',
					background: '#191E24',
					enableScroll: true,
					dataLabel:false,
					fontSize: 11,
					pixelRatio: _self.pixelRatio,
					animation: true,
					categories: data.categories, //数据类别(饼图、圆环图不需要)
					series: data.series, //	数据列表
					xAxis: {
						"boundaryGap": "justify",
						gridType: 'solid',
						gridColor: '#2C333C',
						fontColor: '#FFFFFF',
						axisLineColor: '#2C333C',
						itemCount:8
					},
					legend: {
						show: false,
					},
					yAxis: {
						showTitle: true,
						data: [{
							position: 'right',
							min: 0,
							max: 100,
							title: 'km',
							axisLineColor: '#2C333C',
							format: (val) => {
								return val.toFixed(0) + '%'
							}
						}],
						gridColor: '#2C333C',
						gridType: 'solid',
						splitNumber: 2
					},
					extra: {
						area: {
							addLine: true,
							gradient: true
						}
					},
					padding: [15, 0, 0, 15],
					width: _self.cWidth * _self.pixelRatio,
					height: _self.cHeight * _self.pixelRatio
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

		.content {
			width: 100%;
			height: 100%;
			padding: 20rpx 0;
			.charts-box {
				  width: 100%;
				  height: 800rpx;
			}
		}
	}
</style>
