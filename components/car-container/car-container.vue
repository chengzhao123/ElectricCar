<template>
	<view class="car-container" :style="[contentStyle]">
		<scroll-view class="car-container-scroll" :scroll-x="scrollX" :scroll-y="scrollY"
			:scroll-with-animation="scrollwithanimation" :refresher-enabled="refresher"
			:refresher-background="refresherBackground" :refresher-triggered="triggered"
			@refresherpulling="onScrollPulling" @refresherrefresh="onScrollRefresh" @refresherrestore="onScrollRestore"
			:show-scrollbar="showscrollbar" @refresherabort="onScrollAbort"
			@scroll="onScroll" :isCanRefresher="isCanRefresher">
			<view id="car-container-content">
				<slot />
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		name: 'car-container',
		data() {
			return {
				top: 0,
				refresher: false,
				refreshing: false
			}
		},
		props: {
			scrollX: {
				type: Boolean,
				default: false
			},
			scrollY: {
				type: Boolean,
				default: false
			},
			// 重要！！！ 是否能够下拉刷新
			isCanRefresher: {
				type: Boolean,
				default: false
			},
			showscrollbar: {
				type: Boolean,
				default: false
			},
			scrollwithanimation: {
				type: Boolean,
				default: false
			},
			refresherBackground: {
				type: String,
				default: '#191E24'
			},
			triggered: {
				type: Boolean,
				default: false
			},
			contentStyle: {
				type: Object,
				default: function() {
					return {}
				}
			}
		},
		mounted() {
			uni.createSelectorQuery().in(this).select(`#car-container-content`).boundingClientRect().exec(ret => {
				this.top = ret[0].top;
				if ((ret[0].height <= uni.getSystemInfoSync().windowHeight) && this.isCanRefresher) {
					this.refresher = true
				}
			});
		},
		methods: {
			onScrollPulling(e) {
				let self = this;
				self.$emit('pulling', e);
			},
			// 刷新
			onScrollRefresh() {
				let self = this;
				self.$emit('refresh');
			},

			onScrollRestore(e) {
				let self = this;
				self.$emit('restore', e);
			},

			onScrollAbort(e) {
				let self = this;
				self.$emit('abort', e);
			},
			/**滚动到底部 */
			// onScrollBottom(e) {
			// 	let self = this;
			// 	self.$emit('tolower', e);
			// },
			/**滑动*/
			onScroll(e) {
				let self = this;
				setTimeout(() => {
					uni.createSelectorQuery()
						.in(self)
						.select(`#car-container-content`)
						.boundingClientRect()
						.exec(ret => {
							if ((ret[0].height <= uni.getSystemInfoSync().windowHeight) && this.isCanRefresher) {
								this.refresher = true
							}
							self.refresher = false
							let topDistance = ret[0].top - self.top
							if (parseInt(topDistance) == 0) {
								self.$emit('toupper', e);
								if (this.isCanRefresher) {
									self.refresher = true
								}
								console.log('到顶')
								uni.showToast({
									icon: 'none',
									duration: 600,
									title: '到顶了'
								})
							}
							// console.log(ret[0].top,self.top)
							console.log(ret[0].bottom,uni.getSystemInfoSync().windowHeight)
							let btmDistance = ret[0].bottom - uni.getSystemInfoSync().windowHeight
							if (parseInt(btmDistance) == 0) {
								self.$emit('tolower', e);
								console.log('到底')
								uni.showToast({
									icon: 'none',
									duration: 600,
									title: '到底了'
								})
							}
						});
				}, 20);
				self.$emit('scroll', e);
			}
		}
	}
</script>

<style lang="scss" scoped>
	.car-container {
		position: relative;

		.car-container-scroll {
			width: 100%;
			height: 100%;
		}
	}
</style>
