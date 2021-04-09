<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="个人资料" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<car-cell isArrow cellColor="#22282F" marginTB @jump="setAvatar">
					<view slot="left">头像</view>
					<view slot="right">
						<image v-if="!avatar" style="width: 90rpx; height: 90rpx; border-radius: 50%;"
							src="/static/images/icons/my/logo.png" mode="scaleToFill"></image>
						<image v-else style="width: 90rpx;height: 90rpx; border-radius: 50%;"
							:src="avatar" mode="scaleToFill"></image>
					</view>
				</car-cell>
				<car-cell isArrow cellColor="#22282F" @jump="setNickName">
					<view slot="left">昵称</view>
					<view slot="right"><text>疯狂的鸭子</text></view>
				</car-cell>
				<car-cell isArrow cellColor="#22282F" @jump="setPhone">
					<view slot="left">手机号</view>
					<view slot="right"><text>159 2895 3344</text></view>
				</car-cell>
				<car-cell isArrow cellColor="#22282F" @jump="setEmail">
					<view slot="left">邮箱</view>
					<view slot="right"><text>374176450@qq.com</text></view>
				</car-cell>
				<car-cell isArrow cellColor="#22282F" marginTB @jump="clickBir">
					<view slot="left">生日</view>
					<view slot="right">
						<text>{{time}}</text>
					</view>
				</car-cell>
				<car-cell isArrow cellColor="#22282F" @jump="setAdress">
					<view slot="left">收货地址</view>
				</car-cell>
				<w-picker ref="picker" :visible.sync="visible" mode="date" fields="day" :value="time" current
					@confirm="onConfirm($event,'date')" @cancel="onCancel"></w-picker>
			</view>
		</car-container>
		<view v-if="showModel" class="model" @click.stop="showModel = false">
			<view @click="sureAvatar" class="btn">
				<text class="bind">保存</text>
			</view>
			<image class="img" :src="avatarurl" mode="f"></image>
		</view>
	</view>
</template>

<script>
	import dayjs from 'dayjs'
	export default {
		name: 'Info',
		data() {
			return {
				time: dayjs(new Date().getTime()).format('YYYY-MM-DD'),
				visible: false,
				avatar: null,
				avatarurl: null,
				showModel: false
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
		},
		methods: {
			onConfirm(e) {
				this.time = dayjs(e.value).format('YYYY-MM-DD')
			},
			onCancel() {
				this.$refs.picker.hide()
			},
			clickBir() {
				this.$refs.picker.show()
			},
			back() {
				uni.navigateBack()
			},
			setEmail() {
				uni.navigateTo({
					url: '/pages/my/info/setEmail/index'
				})
			},
			setNickName() {
				uni.navigateTo({
					url: '/pages/my/info/nickName/index'
				})
			},
			setAdress() {
				uni.navigateTo({
					url: '/pages/my/info/adress/index'
				})
			},
			setPhone() {
				uni.navigateTo({
					url: '/pages/my/info/phone/index'
				})
			},
			sureAvatar() {
				this.showModel = false
				this.avatar = this.avatarurl
			},
			// 修改头像
			setAvatar() {
				uni.chooseImage({
					count: 1,
					success: async (ev) => {
						console.log(ev)
						this.avatarurl = ev.tempFilePaths[0]
						this.showModel = true
					},
					fail: (ev) => {
						uni.showToast({
							title: '修改头像失败',
							duration: 1000,
							icon: 'none'
						})
					}
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
			box-sizing: border-box;
			padding: 20rpx 0;
		}

		.model {
			position: absolute;
			top: 0;
			right: 0;
			bottom: 0;
			left: 0;
			z-index: 1000;
			background-color: #343434;
			.btn {
				position: absolute;
				right: 32rpx;
				top: 100rpx;
				width: 110rpx;
				height: 60rpx;
				text-align: center;
				line-height: 60rpx;
				border-radius: 12rpx;
				background-color: #2A77FF;
			
				.bind {
					font-size: 32rpx;
					color: #FFFFFF;
				}
			}
			.img {
				top: 25vh;
				bottom: 25vh;
				width: 100vw;
				max-height: 50vh;
				overflow: hidden;
			}
		}
	}
</style>
