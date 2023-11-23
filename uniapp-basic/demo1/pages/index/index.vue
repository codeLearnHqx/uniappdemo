<template>
	<view class="box">
		<view  v-html="code"></view>
		<navigator open-type="switchTab" url="/pages/list/list?wd=uniapp">
			<button type="primary">新闻页</button>
		</navigator>
		<navigator open-type="reLaunch" url="/pages/about/about">
			<button type="primary">关于页</button>
		</navigator>
		<test/>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				code: '<h1 onclick="javascript: alert(1)">111</h1>'
			}
		}
	}
</script>

<style lang="scss">
</style>