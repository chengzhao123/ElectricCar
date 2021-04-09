<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="在线客服" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style" @refresh="onRefresh" :triggered="triggered" isCanRefresher>
			<view class="content" @click.stop="isClick = false">
				<view class="cu-chat">
					<view class="items">
						<view class="avatars"
							style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big143004.jpg);">
						</view>
						<view class="mains">
							<view class="nickname">小电驴</view>
							<view class="writeContent">
								<text>我是客服小电驴，请问有什么可 以帮到您的？</text>
							</view>
						</view>
					</view>
					<view class="items self">
						<view class="mains">
							<view class="actions">
								<text class="cuIcon-loading cuIcon del"></text>
							</view>
							<view class="writeContent">你好!!!!!</view>
						</view>
						<view class="avatars"
							style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big107000.jpg);">
						</view>
					</view>
					<view class="items self">
						<view class="mains">
							<image src="https://ossweb-img.qq.com/images/lol/web201310/skin/big10006.jpg" class="radius"
								mode="widthFix"></image>
						</view>
						<view class="avatars"
							style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big107000.jpg);">
						</view>
					</view>
					<view class="dates"> 下午13:23</view>
					<view class="items">
						<view class="avatars"
							style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big143004.jpg);">
						</view>
						<view class="mains">
							<view class="nickname">小电驴</view>
							<view class="writeContent">
								<text>我是客服小电驴，请问有什么可 以帮到您的？</text>
							</view>
						</view>
					</view>
					<view class="items">
						<view class="avatars"
							style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big143004.jpg);">
						</view>
						<view class="mains">
							<view class="nickname">小电驴</view>
							<view class="writeContent">
								<text>我是客服小电驴，请问有什么可 以帮到您的？</text>
							</view>
						</view>
					</view>
					<view class="items self">
						<view class="mains">
							<view class="actions">
								<text class="cuIcon-loading cuIcon del"></text>
							</view>
							<view class="writeContent">你好!!!!!</view>
						</view>
						<view class="avatars"
							style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big107000.jpg);">
						</view>
					</view>
				</view>

				
			</view>
		</car-container>
		<!-- 底部导航栏 -->
		<view class="sendArea" @click.stop="">
			<view class="notShow">
				<view class="inputA">
					<input class="solid-bottom" @focus="InputFocus" @blur="InputBlur" maxlength="300" />
				</view>
				<view class="addbtn text-white" v-if="!isFocus" @click.stop="isClick = true">
					<text class="cuIcon cuIcon-roundadd"></text>
				</view>
				<button v-else class="cu-btn sendBtn">发送</button>
			</view>
			<view class="show" v-if="isClick">
				<view class="actionArea">
					<view class="itemMx" v-for="(item, index) in 2" :key="index" @click="dianji(index)">
						<view class="imgAr">
							<image class="ig" src="/static/images/icons/my/logo.png" mode="scaleToFill" />
						</view>
						<text>图片</text>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name: 'ChatIndex',
		data() {
			return {
				triggered: false,
				isFocus: false,
				isClick: false,
				avatar: null
			}
		},

		computed: {
			Style() {
				let style = {
					'height': "calc(100vh - " + this.CustomBar * 2 + 'rpx' + ")"
				}
				return style
			},
		},
		methods: {
			back() {
				uni.navigateBack()
			},
			InputFocus() {
				this.isFocus = true
			},
			InputBlur() {
				this.isFocus = false
			},
			dianji(index) {
				if (index == 0) {
					uni.chooseImage({
						count: 1,
						success: async (ev) => {
							console.log(ev)
							this.avatar = ev.tempFilePaths[0]
							// this.showModel = true
						},
						fail: (ev) => {
							uni.showToast({
								title: '无法上传图片',
								duration: 1000,
								icon: 'none'
							})
						}
					})
				}
			},
			initData() {
				setTimeout(() => {
					this._refreshing = false
					this.triggered = false
					console.log('刷新')
				}, 1000)
			},
			onRefresh() {
				if (this._refreshing) return
				this._refreshing = true;
				this.triggered = true;
				this.initData();
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
			background-color: #191E24;
			padding-bottom: 140rpx;

			.dates {
				display: flex;
				justify-content: center;
				font-size: 24rpx;
				margin-top: 46rpx;
				color: #AAAAAA;
				position: relative;
				width: calc(100% - 320rpx);
				left: 160rpx;
			}

			.items {
				display: flex;
				padding: 30rpx 30rpx 10rpx;
				position: relative;

				.mains {
					max-width: calc(100% - 260rpx);
					display: flex;
					flex-direction: column;
					justify-content: flex-start;
					align-items: flex-start;
					margin: 0 20rpx;

					.actions {
						padding-right: 20rpx;
						display: flex;
						align-items: center;

						.del {
							color: #FF4040;
						}
					}

					.nickname {
						font-size: 26rpx;
						color: #69707C;
						margin-bottom: 12rpx;
					}

					.writeContent {
						padding: 20rpx;
						border-top-left-radius: 0;
						border-top-right-radius: 12rpx;
						border-bottom-left-radius: 12rpx;
						border-bottom-right-radius: 12rpx;
						display: inline-flex;
						max-width: 100%;
						align-items: center;
						font-size: 30rpx;
						position: relative;
						min-height: 80rpx;
						line-height: 40rpx;
						text-align: left;
						background-color: #22282F;
						color: #FFFFFF;
					}
				}

				.avatars {
					font-variant: small-caps;
					margin: 0;
					padding: 0;
					display: inline-flex;
					text-align: center;
					justify-content: center;
					align-items: center;
					background-color: #ccc;
					color: #ffffff;
					white-space: nowrap;
					position: relative;
					width: 80rpx;
					height: 80rpx;
					background-size: cover;
					background-position: center;
					vertical-align: middle;
					border-radius: 50%;
				}

			}

			.self {
				// padding: 80rpx 30rpx 10rpx;
				justify-content: flex-end;
				text-align: right;

				.mains {
					flex-direction: row;
					justify-content: flex-end;
					align-items: center;
				}
			}

			.self>.mains>.writeContent {
				background-color: #2A77FF;
				border-top-left-radius: 12rpx;
				border-top-right-radius: 0;
				border-bottom-left-radius: 12rpx;
				border-bottom-right-radius: 12rpx;
			}
		}
		
		.sendArea {
			background-color: #2E343C;
			position: fixed;
			width: 100%;
			bottom: 0;
			z-index: 1024;
			box-shadow: 0, -0.5px, 3px, rgba(0, 0, 0, 0.1);
			min-height: 50px;
		
			input {
				overflow: initial;
				line-height: 32px;
				height: 32px;
				min-height: 32px;
				flex: 1;
				font-size: 15px;
				margin: 0 10px;
			}
		
			.notShow {
				display: flex;
				align-items: center;
				justify-content: space-between;
		
				.inputA {
					width: 100%;
					margin: 20rpx 0 16rpx 32rpx;
					border-radius: 32rpx;
					background-color: #191E24;
				}
		
				.addbtn {
					font-size: 64rpx;
					margin: 0 32rpx;
				}
		
				.sendBtn {
					white-space: nowrap;
					font-size: 28rpx;
					color: #FFFFFF;
					background-color: #2A77FF;
					margin: 0 32rpx;
				}
			}
		
			.show {
				max-height: 282rpx;
				overflow-x: scroll;
				overflow-y: hidden;
		
				.actionArea {
					padding: 60rpx 0;
					display: flex;
					justify-content: flex-start;
					align-items: center;
					flex-wrap: nowrap;
					width: max-content;
		
					.itemMx {
						display: flex;
						flex-direction: column;
						justify-content: center;
						align-items: center;
						margin-left: 60rpx;
		
						.imgAr {
							position: relative;
							background-color: #191E24;
							padding: 30rpx;
		
							.ig {
								width: 60rpx;
								height: 60rpx;
							}
						}
		
						text {
							margin-top: 20rpx;
							color: #FFFFFF;
							font-size: 26rpx;
						}
					}
		
					.itemMx:last-child {
						margin-right: 60rpx;
					}
				}
			}
		}
	}
</style>
