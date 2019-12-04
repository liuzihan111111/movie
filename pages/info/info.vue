<template>
	<view class="content">
		<view class="title">{{title}}...</view>
		<rich-text class="art-content" :nodes="content"></rich-text>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				image:'',
				title:'',
				content:""
			}
		},
		onLoad(e) {
			console.log(e)
			uni.showLoading({
				title:"加载中...."
			})
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news/36kr/'+e.newsid,
				method: 'GET',
				data: {},
				success: res => {
				//	console.log(res)
					//this.image=res.data.author_avatar;
					this.image=res.data.cover;
					this.title=res.data.title;
					this.content=res.data.content;
					uni.hideLoading()
				},
				fail: () => {
					uni.hideLoading()
				},
				complete: () => {}
			});
		},
		methods: {
			
		}
	}
</script>

<style>
.content{padding:10upx 2%; width: 96%; flex-wrap:wrap; }
.title{line-height:2em; font-weight:700; font-size:38upx;}
.art-content{line-height:2em;}
</style>
