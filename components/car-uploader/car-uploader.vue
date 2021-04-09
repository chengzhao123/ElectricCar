<template>
	<view class="van-uploader">
		<view class="van-uploader__wrapper">
			<!-- 预览样式 -->
			<view v-if=" previewImage " v-for="(item,index) in lists" :key="index" class="van-uploader__preview">
				<image v-if="item.isImage" :mode="imageFit" :src="item.url || item.path" :alt="item.name || ('图片' + index)" class="van-uploader__preview-image"
				 :style="[style]" :data-url="item.url || item.path" @click="doPreviewImage" />
				<view v-else class="van-uploader__file" :style="[style]">
					<!-- <van-icon name="description" class="van-uploader__file-icon" /> -->
					<view class="van-uploader__file-name van-ellipsis">{{ item.name || item.url || item.path }}</view>
				</view>
				<!-- <icon v-if="deletable" :type="'clear'" size="16" class="van-uploader__preview-delete" :data-index="index" @click="deleteItem"></icon> -->
				<text v-if="deletable" class="van-uploader__preview-delete cuIcon cuIcon-close" :data-index="index" @click="deleteItem"></text>
			</view>

			<!-- 上传样式 -->
			<block v-if="isInCount">
				<view v-if="useSlot" class="van-uploader__slot" @click="startUpload">
					<slot />
				</view>

				<!-- 默认上传样式 -->
				<view v-else class="van-uploader__upload" :style="[style]" @click="startUpload">
					<text v-if="uploadText" class="van-uploader__upload-text">{{ uploadText }}</text>
				</view>
			</block>
		</view>
	</view>
</template>

<script>
	// import {
	// 	addUnit
	// } from '@/common/lib';

	import {
		isImageFile,
		chooseFile,
	} from './utils';
	export default {
		name: "wmUploader",
		props: {
			disabled: Boolean,
			multiple: Boolean,
			uploadText: String,
			useSlot: Boolean,
			useBeforeRead: Boolean,
			previewSize: {
				type: [Number, Object],
				default: 90
			},
			name: {
				type: [Number, String],
				default: ''
			},
			accept: {
				type: String,
				default: 'image'
			},
			fileList: {
				type: Array,
				default: []
			},
			maxSize: {
				type: Number,
				default: Number.MAX_VALUE
			},
			maxCount: {
				type: Number,
				default: 100
			},
			deletable: {
				type: Boolean,
				default: true
			},
			previewImage: {
				type: Boolean,
				default: true
			},
			previewFullImage: {
				type: Boolean,
				default: true
			},
			imageFit: {
				type: String,
				default: 'scaleToFill'
			}
		},
		data() {
			return {
				lists: [],
				isInCount: 0,
				computedPreviewSize: null
			};
		},
		created() {
			this.formatFileList()
		},
		computed: {
			style() {
				let style = {};
				console.log(this.previewSize,this.previewSize.constructor === Object)
				if (this.previewSize.constructor === Object) {
					if (this.previewSize.height) {
						style.height = this.previewSize.height + 'px';
					}
					if (this.previewSize.width) {
						style.width = this.previewSize.width + 'px';
					}
				} else {
					style = {
						width: this.previewSize + 'px',
						height: this.previewSize + 'px'
					}
				}
				return style;
			}
		},
		watch: {
			fileList: {
				handler: function(val, oldval) {
					this.formatFileList()
				},
				deep: true //对象内部的属性监听，也叫深度监听
			},
			name() {
				this.formatFileList()
			}
		},
		methods: {
			formatFileList() {
				console.log("formatFileList")
				const fileList = this.fileList,
					maxCount = this.maxCount

				const lists = fileList.map(item => (Object.assign(Object.assign({}, item), {
					// isImage: typeof item.isImage === 'undefined' ? isImageFile(item) : item.isImage //原来的
					isImage: typeof item === 'undefined' ? isImageFile(item) : item //自己写的
				})));
				this.lists = lists
				this.isInCount = lists.length < maxCount
			},
			startUpload() {
				if (this.disabled)
					return;
				const
					name = this.name,
					capture = ['album', 'camera'],
					maxCount = this.maxCount,
					multiple = this.multiple,
					maxSize = this.maxSize,
					accept = this.accept,
					lists = this.lists,
					useBeforeRead = this.useBeforeRead;

				let chooseFile = null;
				const newMaxCount = maxCount - lists.length;
				// 设置为只选择图片的时候使用 chooseImage 来实现
				if (accept === 'image') {
					chooseFile = new Promise((resolve, reject) => {
						uni.chooseImage({
							count: multiple ? (newMaxCount > 9 ? 9 : newMaxCount) : 1,
							sourceType: capture,
							success: resolve,
							fail: reject
						});
					});
				} else {
					chooseFile = new Promise((resolve, reject) => {
						uni.chooseMessageFile({
							count: multiple ? newMaxCount : 1,
							type: 'file',
							success: resolve,
							fail: reject
						});
					});
				}
				chooseFile.then((res) => {
					const file = multiple ? res.tempFiles : res.tempFiles[0];
					// 检查文件大小
					if (file instanceof Array) {
						const sizeEnable = file.every(item => item.size <= maxSize);
						if (!sizeEnable) {
							this.$emit('oversize', {
								name
							});
							return;
						}
					} else if (file.size > maxSize) {
						this.$emit('oversize', {
							name
						});
						return;
					}
					// 触发上传之前的钩子函数
					if (useBeforeRead) {
						this.$emit('before-read', {
							file,
							name,
							callback: (result) => {
								if (result) {
									// 开始上传
									this.$emit('after-read', {
										file,
										name
									});
								}
							}
						});
					} else {
						this.$emit('after-read', {
							file,
							name
						});
					}
				});
			},
			deleteItem(event) {
				const {
					index
				} = event.currentTarget.dataset;
				this.$emit('delete', {
					index,
					name: this.name
				});
			},
			doPreviewImage(event) {
				if (!this.previewFullImage)
					return;
				const curUrl = event.currentTarget.dataset.url;
				const images = this.lists
					.filter(item => item.isImage)
					.map(item => item.url || item.path);
				this.$emit('click-preview', {
					url: curUrl,
					name: this.name
				});
				uni.previewImage({
					urls: images,
					current: curUrl,
					fail() {
						uni.showToast({
							title: '预览图片失败',
							icon: 'none'
						});
					}
				});
			}
		}
	}
</script>

<style scoped lang="scss">
	.van-uploader {
		position: relative;
		display: inline-block
	}

	.van-uploader__wrapper {
		display: -webkit-flex;
		display: flex;
		-webkit-flex-wrap: wrap;
		flex-wrap: wrap
	}

	.van-uploader__upload {
		font-weight: lighter;
		position: relative;
		display: -webkit-flex;
		display: flex;
		-webkit-flex-direction: column;
		flex-direction: column;
		-webkit-align-items: center;
		align-items: center;
		-webkit-justify-content: center;
		justify-content: center;
		box-sizing: border-box;
		width: 80px;
		height: 80px;
		margin: 0 8px 8px 0;
		background-color: transparent;
		border: 1px dashed #FFFFFF;
		border-radius: 4px
	}

	.van-uploader__upload-icon {
		display: inline-block;
		width: 24px;
		height: 24px;
		color: #FFFFFF;
		font-size: 24px
	}

	.van-uploader__upload-text {
		display: flex;
		justify-content: space-between;
		align-items: center;
		// margin-top: -20px;
		color: #D8D8D8;
		font-size: 32px
	}

	.van-uploader__preview {
		position: relative;
		margin: 0 8px 8px 0
	}

	.van-uploader__preview-image {
		display: block;
		width: 80px;
		height: 80px;
		border-radius: 4px
	}

	.van-uploader__preview-delete {
		position: absolute;
		top: -8px;
		right: -8px;
		color: #FFFFFF;
		font-size: 12px;
		padding: 4px;
		text-align: center;
		line-height: 100%;
		background-color: #EC3E55;
		border-radius: 100%
	}

	.van-uploader__file {
		display: -webkit-flex;
		display: flex;
		-webkit-flex-direction: column;
		flex-direction: column;
		-webkit-align-items: center;
		align-items: center;
		-webkit-justify-content: center;
		justify-content: center;
		width: 80px;
		height: 80px;
		background-color: #f7f8fa;
		border-radius: 4px
	}

	.van-uploader__file-icon {
		display: inline-block;
		width: 20px;
		height: 20px;
		color: #646566;
		font-size: 20px
	}

	.van-uploader__file-name {
		box-sizing: border-box;
		width: 100%;
		margin-top: 8px;
		padding: 0 5px;
		color: #646566;
		font-size: 12px;
		text-align: center
	}
</style>
