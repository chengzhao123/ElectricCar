<template>
	<view class="mf">
		<car-nav-bar isBack @back="back" title="修改密码" backColor="#22282F">
			<view slot="left"><text class="cuIcon cuIcon-back"></text></view>
			<view slot="right"><text>保存</text></view>
		</car-nav-bar>
		<car-container scrollY :contentStyle="Style">
			<view class="content">
				<car-cell cellColor="#22282F">
					<view slot="left"><span class="oneTitle">新密码</span></view>
					<view slot="center">
						<input class="newPwd" type="password" placeholder="新密码" value="15928953344" maxlength="15" />
					</view>
					<view slot="right"><image class="dela" src="/static/images/icons/my/del.png" mode="widthFix" @click="deleteValue"></image></view>
				</car-cell>
				<car-cell cellColor="#22282F">
					<view slot="left"><span class="oneTitle">确认密码</span></view>
					<view slot="center">
						<input class="newPwd2" type="password" placeholder="确认密码" value="15928953344" maxlength="15" />
					</view>
					<view slot="right"><image class="dela" src="/static/images/icons/my/del.png" mode="widthFix" @click="deleteValue"></image></view>
				</car-cell>
			</view>
		</car-container>
	</view>
</template>

<script>
	export default {
		name: 'NewPassWd',
		data() {
			return {
				
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
		methods:{
			back() {
				uni.navigateBack()
			},
			deleteValue() {
				console.log('删除')
			},
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
			padding: 32rpx 0;
			.dela {
				width: 32rpx;
			}
			.num {
				font-size: 32rpx;
			}
			.newPwd {
				margin: 0 100rpx;
				font-size: 32rpx;
			}
			.newPwd2 {
				margin: 0 100rpx 0 74rpx;
				font-size: 32rpx;
			}
		}
	}
</style>
