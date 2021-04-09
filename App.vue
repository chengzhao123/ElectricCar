<script>
	import Vue from 'vue';
	export default {
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		},
		onLaunch() {
			uni.getSystemInfo({
				success: function(e) {
					Vue.prototype.System = e
					Vue.prototype.WindowHeight = e.windowHeight;
					Vue.prototype.windowWidth = e.windowWidth;
					// #ifndef MP
					Vue.prototype.StatusBar = e.statusBarHeight;
					if (e.platform == 'android') {
						Vue.prototype.CustomBar = e.statusBarHeight + 50;
					} else {
						Vue.prototype.CustomBar = e.statusBarHeight + 45;
					};
					// #endif
			
					// #ifdef H5
					Vue.prototype.Platform = 3001
					// #endif
					// #ifdef APP-PLUS
					Vue.prototype.Platform = 3001
					// #endif
					// #ifdef MP
					Vue.prototype.Platform = 3002
					// #endif
			
					// #ifdef MP-WEIXIN
					Vue.prototype.StatusBar = e.statusBarHeight;
					let custom = wx.getMenuButtonBoundingClientRect();
					Vue.prototype.Custom = custom;
					Vue.prototype.CustomBar = custom.bottom + custom.top - e.statusBarHeight;
					// #endif		
			
					// #ifdef MP-ALIPAY
					Vue.prototype.StatusBar = e.statusBarHeight;
					Vue.prototype.CustomBar = e.statusBarHeight + e.titleBarHeight;
					// #endif
					// console.log("CustomBar", Vue.prototype.CustomBar)
					// TODO：底部导航栏的高度
					Vue.prototype.CustomTabBar = 50;
			
					//实际像素与设计像素比率
					Vue.prototype.PixelRatio = parseFloat(e.windowWidth) / parseFloat(375);
				},
			})
		}
	}
</script>

<style lang="scss">
	/* #ifndef APP-NVUE */
		@import 'colorui/main.css';
		@import 'colorui/icon.css';
	/* #endif */
	input {
		/* #ifndef APP-NVUE */
		caret-color: #2A77FF;
		/* #endif */
	}

	/*每个页面公共css */
</style>
