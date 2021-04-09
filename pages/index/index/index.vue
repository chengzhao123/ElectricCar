<template>
	<view class="mf">
		<car-nav-bar isBack title="这是头部">
			<view slot="left">返回首页</view>
			<view slot="right">添加好友</view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'Index',
		data() {
			return {
				
			}
		},
		onLoad() {

		},
		computed: {
			Style() {
				let style = {
					'height': 'calc(100vh - 200rpx)'
				}
				return style
			}
		},
		methods: {

		}
	}
</script>

<style lang="scss" scoped>
.mf {
	width: 100%;
	height: 100%;
}
</style>
