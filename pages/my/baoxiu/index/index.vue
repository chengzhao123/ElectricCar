<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="在线报修" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<car-cell isArrow cellColor="#22282F" class="cell">
					<view slot="left">优先网点</view>
					<view slot="right"><input class="input" type="text" v-model="one" maxlength="8" /></view>
				</car-cell>
				<car-cell isArrow cellColor="#22282F" class="cell">
					<view slot="left">报修人</view>
					<view slot="right"><input class="input" type="text" v-model='two' /></view>
				</car-cell>
				<view class="detail">
					<view class="dTitle">请描述你的问题</view>
					<textarea
						class="area"
						maxlength="200"
						v-model="detailInfo" 
						placeholder="为更好的服务您，请输入至少4个紫的故障描述，您可以说：“车子的XX部位出现了XX的问题”。"
					/>
					<view class="countComp"><text>{{numCmp}}</text>/200</view>
				</view>
				<view class="picArea">
					<view class="dTitle">
						<text class="t">上传图片</text>
						<text class="n">{{picNum}}/9</text>
					</view>
					<view class="picUpload">
						<car-uploader :file-list="list" :previewSize="imgWidHei" :maxCount="9" use-before-read :uploadText="'+'" @before-read="onBeforeRead"
						 @after-read="onAfterRead" @delete="uploaderDelete">
						</car-uploader>
					</view>
				</view>
				
				<view class="btmArea">
					<view class="btn cu-btn block" @click="goSuccess">
						<text class="bind">立即提交</text>
					</view>
				</view>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'OnlineXiuIndex',
		data() {
			return {
				imgWidHei: {width:108,height:108},
				one: '自动分配',
				two: '请填写以保证服务质量',
				num: 0,
				detailInfo: '',
				list: []
			}
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
			numCmp() {
				return this.detailInfo.length
			},
			picNum() {
				return this.list.length
			}
		},
		methods: {
			back() {
				uni.navigateBack()
			},
			goSuccess() {
				uni.navigateTo({
					url: '/pages/my/baoxiu/success/index'
				})
			},
			// 上传图片相关
			async onBeforeRead(event) {
				console.log("onBeforeRead", event)
				const callback = event.callback
				callback(true)
			},
			// TODO：文件选取之后，执行上传，替换路由
			async onAfterRead(event) {
				let file = event.file
				// await storage.upload(1, file.path, function(res) {
				// 	uni.showLoading({
				// 		title:"上传中"+res.progress+"%"
				// 	})
				// }).then(res => {
				// 	self.list.push({path: res.data})
				// 	self.$forceUpdate()
				// 	uni.hideLoading()
				// }).catch(res => {
				// 	uni.hideLoading()
				this.list.push({path: event.file.path })
				// })
			},
			uploaderDelete(ev){
				this.list.splice(ev.index, 1)
			}
		}
		
	}
</script>

<style lang="scss" scoped>
	.van-uploader__upload {
		background-color: transprent !important;
	}
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
			padding-top: 20rpx;
			padding-bottom: 120rpx;
			.detail {
				position: relative;
				width: 100%;
				height: 340rpx;
				padding: 20rpx 32rpx;
				font-size: 28rpx;
				color: #FFFFFF;
				background-color: #22282F;
				margin: 20rpx 0;
				.dTitle {
					margin-bottom: 20rpx;
				}
				.area {
					margin-top: 20rpx;
					width: 100%;
					height: 160rpx;
					overflow: auto;
					color: #69707C;
					font-size: 28rpx;
				}
				.countComp {
					position: absolute;
					right: 32rpx;
					bottom: 32rpx;
					color: #69707C;
					font-size: 28rpx;
				}
			}
			.picArea {
				padding: 20rpx 32rpx;
				background-color: #22282F;
				margin-bottom: 32rpx;
				.dTitle {
					margin: 30rpx 0;
					display: flex;
					justify-content: space-between;
					align-items: center;
					font-size: 28rpx;
					.t {
						color: #FFFFFF;
					}
					.n {
						color: #69707C;
					}
				}
			}
			.cell {
				border-radius: 16rpx;
				margin-bottom: 20rpx;
				.areaName {
					font-size: 28rpx;
					color: #69707C;
					white-space: nowrap;
				}
				.input {
					color: #69707C;
					text-align: right;
					font-size: 28rpx;
				}
			}
			.btmArea {
				position: fixed;
				left: 0;
				right: 0;
				background-color: #191E24;
				bottom: 0;
			}
			.btn {
				position: relative;
				margin: 0 32rpx 28rpx 32rpx;
				height: 100rpx;
				border-radius: 12rpx;
				background-color: #2A77FF;
				.bind {
					font-size: 32rpx;
					color: #FFFFFF;
				}
			}
		}
	}
</style>
