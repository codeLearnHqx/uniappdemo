<template>
	<view>
		<button v-if="show" type="primary" @click="getDetail()">重新加载</button>
		<view v-else>
			<view class="detail">
				<view class="title">{{item.title}}</view>
				<view class="content">{{item.body}}</view>
			</view>
			<view class="comments">
				<view class="text">讨论</view>
				<view class="row" v-for="comment in comments" :key="comment.id">
					<view class="top">
						<view class="name">{{comment.name}}</view>
						<view class="email">{{comment.email}}</view>
					</view>
					<view class="body">
						{{comment.body}}
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				titleId: '',
				item: {},
				comments: [],
				show: false
			}
		},
		onLoad(e) {
			this.titleId = e.id
			this.getDetail()
			this.getComments()
		},
		methods: {
			getDetail() {
				uni.showLoading({
					title: '加载内容中...'
				})
				uni.request({
					url: `https://jsonplaceholder.typicode.com/posts/${this.titleId}`,
					timeout: 3000,
					success: res => {
						this.item = res.data
						this.show = false
					},
					fail: () => {
						console.log('请求出错了，请重试')
						this.show = true
					},
					complete: () => {
						uni.hideLoading()
					}
				})
			},
			getComments() {
				uni.request({
					url: `https://jsonplaceholder.typicode.com/posts/${this.titleId}/comments`,
					success: (res) => {
						this.comments = res.data
					}
				})
			}
		}
	}
</script>

<style lang="scss">
	.detail {
		padding: 30rpx;
		.title {
			font-size: 46rpx;
			color: #000;
			padding-bottom: 20rpx;
		}
		.content {
			font-size: 30rpx;
			color: #666;
			padding-bottom: 60rpx;
		}
		
	}
	.comments {
		padding: 30rpx;
		background: #f8f8f8;
		.text {
			font-size: 46rpx;
			margin-bottom: 30rpx;
		}
		.row {
			border-bottom: 1rpx solid #e8e8e8;
			padding: 20rpx 0;
			.top {
				display: flex;
				justify-content: space-between;
				font-size: 22rpx;
				color: #999;
				padding-bottom: 15rpx;
			}
			.body {
				font-size: 28rpx;
				color: #555;
			}
		}
	}
</style>
