<template>
	<car-nav-bar isBack @back="back" title="扫码二维码" backColor="#22282F">
		<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
	</car-nav-bar>
</template>

<script>
	export default {
		name: 'Scan',
		data() {
			return {

			}
		},
		
		onLoad() {
			this.loadData()
		},
		methods: {
			loadData() {
				uni.scanCode({
					success: function(res) {
						console.log(res)
						console.log('条码类型：' + res.scanType);
						console.log('条码内容：' + res.result);
					}
				});
			},
			back() {
				uni.navigateBack()
			}
		}
	}
</script>

<style lang="scss" scoped>
</style>
