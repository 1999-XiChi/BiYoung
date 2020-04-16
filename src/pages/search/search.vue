<template>
	<view>
		<zy-search :is-focus="false" :theme="themeClass" :show-want="true" :speechEngine="speechEngine"
		:hot-list="hotList" @getSearchText="getSearchText"></zy-search>
	</view>
</template>

<script>
	import zySearch from '../../components/zy-search/zy-search.vue'
	export default {
		components: {
			zySearch
		},
		data() {
			return {
				themeClass: 'block',
				speechEngine: 'baidu', //语音识别引擎
				hotList: ['1元限免','微课堂','托教“3+1”综合班','纯英语交际班']	//初始化推荐列表
			}
		},
		methods: {
			getSearchText(e) {
				uni.showToast({
					title:'您的搜索信息: ' + e,
					icon:"none"
				})
			}
		},
	}
</script>

<style>
</style>
