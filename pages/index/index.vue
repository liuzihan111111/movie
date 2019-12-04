<template>
	<view class="content">
		<!-- 轮播图 -->
		 <swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration" :circular="true">
			<swiper-item>
				<image src="../../static/img/lunbo1.jpg" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/img/lunbo2.jpg" mode=""></image>
			</swiper-item>
			<swiper-item>
				<image src="../../static/img/lunbo3.jpg" mode=""></image>
			</swiper-item>
		</swiper>
		<!-- 新闻列表 -->
		<view class="uni-list">
			<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in dataList" :key="index" @tap="openInfo" :data-newsId="item.post_id">
				<view class="uni-media-list">
					<image class="uni-media-list-logo" :src="item.author_avatar"></image>
					<view class="uni-media-list-body">
						<view class="uni-media-list-text-top">{{item.title}}</view>
						<view class="uni-media-list-text-bottom uni-ellipsis">{{item.created_at}}</view>
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
				 indicatorDots: true,
				 autoplay: true, // 轮播自动播放
				 interval: 5000, // 间隔多长时间滚动一次
				 duration: 500, // 滑动时间
				 dataList:[], // 新闻 列表
			}
		},
		onLoad() {
			// 调用新闻列表
			this.getNewsList()

		},
		methods: {
			// 新闻列表
			getNewsList(){
				uni.request({
					url: 'https://unidemo.dcloud.net.cn/api/news',
					method: 'GET',
					data: {},
					success: res => {
						console.log(res)
						this.dataList=res.data
					},
					fail: () => {},
					complete: () => {}
				});
			},
			// 跳转到详情页
			openInfo(e){
				var newsId=e.currentTarget.dataset.newsid
				uni.navigateTo({
					url:"../info/info?newsid="+newsId
				})
			}

		}
	}
</script>

<style>
	.content{width: 100%;height:100%;flex-direction: column;}
	.swiper{width: 100%;}
	.swiper image{width:100%}
	.swiper-item{width: 100%;height: 200upx;}
	.uni-media-list-body{height: auto;}
	.uni-media-list-text-top{line-height:1.6em;}
	.uni-list{flex: 1;overflow: auto;}
	.uni-list-cell{background: #fafafa;}
</style>
