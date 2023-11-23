<template>
	<view class="out">
		<view class="row" v-for="item in listArr" :key="item.id" @click="goItemDetail(item.id)">
			<view class="title">{{item.title}}</view>
			<view class="content">{{item.body}}</view>
		</view>
	</view>
</template>

<script>
	export default {
		onLoad() {
			this.getdata()
		},
		data() {
			return {
				listArr: []
			}
		},
		methods: {
			// 获取数据
			getdata() {
				uni.request({
					url: 'https://jsonplaceholder.typicode.com/posts',
					method: 'GET',
					timeout: 5000,
					success: res => {
						this.listArr = res.data
					},
					fail: e => {
						console.log(e)
					},
					complete: () => {
						console.log(11111111111)
					}
				})
			},
			// 跳转详情页
			goItemDetail(id) {
				uni.navigateTo({
					url: `/pages/detail/detail?id=${id}`
				})
			}
		}
	}
</script>

<style lang="scss">
	.out {
		padding: 50rpx 30rpx;
		.row {
			padding: 20rpx 0;
			border-bottom: 1rpx dotted #0000ff;
			margin-bottom: 10rpx;
			.title {
				font-size: 36rpx;
				padding-bottom: 15rpx;
				color: #333;
			}
			.content {
				font-size: 28rpx;
				color: #888;
				white-space: nowrap;
				overflow: hidden;
				text-overflow: ellipsis;
			}
		}
	}
</style>
