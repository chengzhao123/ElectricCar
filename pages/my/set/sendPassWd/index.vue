<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="修改密码" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<view class="cTitle">请输入验证码</view>
				<view class="inputArea">
					<view class="itemInput" v-for="(item, index) in num" :key="index">
						<input type="number" :focus="currentIndex == index" maxlength="1" v-model="item.value" :data-id="index" @input="input" @focus="focus"/>
					</view>
				</view>
				<view class="btn cu-btn block radius" @click="gotoSendNum">
					<text class="bind">{{isSend ? '重新发送验证码' : '发送验证码' }}</text>
				</view>
				<view class="btn2 cu-btn block radius">
					<text class="bind">55</text>
				</view>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'SendPassWd',
		data() {
			return {
				isSend: true,
				currentIndex: 0,
				num:[
					{value: ''},
					{value: ''},
					{value: ''},
					{value: ''},
					{value: ''},
					{value: ''}
				]
			}
		},
		computed:{
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
		},
		onLoad() {
			this.gotoSendNum()
		},
		methods:{
			focus(e) {
				this.currentIndex = e.currentTarget.dataset.id
				if (this.num[this.currentIndex].value.length > 0) this.num[this.currentIndex].value = ''
			},
			input(e) {
				this.currentIndex = e.currentTarget.dataset.id
				if (this.num[this.currentIndex + 1] && this.num[this.currentIndex + 1].value.length <=0) {
					this.currentIndex +=1
				}
			},
			back() {
				uni.navigateBack()
			},
			deleteValue() {
				console.log('删除')
			},
			gotoSendNum() {
				// uni.showToast({
				// 	title: `直接跳转到密码页面`,
				// 	duration: 2000,
				// 	mask: true
				// })
				
				// return
				let model = this.num.every((item => {
					return item.value.length > 0
				}))
				if (!model) {
					uni.showToast({
						mask: true,
						title: '请输入完整的验证码',
						duration: 2000,
						icon: 'none'
					})
					
					return
				}
				uni.navigateTo({
					url: '/pages/my/set/newPassWd/index'
				})
				let sum = 0
				this.num.map((item,index) => {
					sum += Number(item.value) * (Math.pow(10, (5-index)))
				})
				uni.showToast({
					mask: true,
					title: `你的验证码是${sum}`,
					duration: 2000,
					icon: 'none'
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
			position: relative;
			padding: 32rpx;
			.cTitle {
				font-size: 28rpx;
				color: #69707C;
				margin-bottom: 30rpx;
			}
			.inputArea {
				box-sizing: border-box;
				width: 100%;
				display: flex;
				justify-content: space-between;
				align-items: center;
				white-space: nowrap;
				margin-bottom: 36rpx;
				.itemInput {
					width: 100rpx;
					height: 100rpx;
					border: 1px solid #404856;
					background-color: #22282F;
					input {
						width: 100%;
						height: 100%;
						color: #FFFFFF;
						display: flex;
						justify-content: center;
						align-items: center;
						text-align: center;
						font-size: 50rpx;
						font-weight: bolder;
						caret-color: #2A77FF;
					}
				}
			}
			.btn {
				box-sizing: border-box;
				height: 100rpx;
				background-color: #2A77FF;
				.bind {
					font-size: 32rpx;
					color: #FFFFFF;
				}
			}
			.btn2 {
				margin-top: 100rpx;
				opacity: 0.4;
				box-sizing: border-box;
				height: 100rpx;
				background-color: #2A77FF;
				.bind {
					font-size: 32rpx;
					color: #FFFFFF;
				}
			}
		}
	}
</style>
