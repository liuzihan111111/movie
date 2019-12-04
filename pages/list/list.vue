<template>
	<view class="content">
		<view class="uni-list">
			<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in list" :key="index">
				<view class="uni-media-list">
					<image class="uni-media-list-logo" :src="item.img"></image>
					<view class="uni-media-list-body">
						<view class="uni-media-list-text-top">{{item.tCn}}</view>
						<view class="uni-media-list-text-dec">
							{{item.commonSpecial?item.commonSpecial:"暂无描述"}}
						</view>
						<view class="uni-media-list-text-bottom uni-ellipsis">类型：{{item.movieType}}</view>
						<view class="uni-media-list-text-bottom uni-ellipsis">影片时长：{{item.d}}分钟</view> 
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
				list:[]
			}
		},
		onLoad() {
			uni.showLoading({
				title: '加载中....',
			});
			// 列表
			uni.request({
				url: 'https://api-m.mtime.cn/Showtime/LocationMovies.api',
				method: 'GET',
				data: {locationId: 290},
				success: res => {
					console.log(res)
					this.list=res.data.ms;
					uni.hideLoading()
				},
				fail: () => {
					uni.hideLoading()
				},
				complete: () => {}
			});
			
		},
		methods: {
			/* function getMovieHot(cb){
  tools.getFetch('https://api-m.mtime.cn/Showtime/LocationMovies.api', { locationId: 290 }, cb)
}  */
		}
	}
</script>

<style>
.uni-list-cell{padding: 15upx 0;border-bottom: 1upx solid #cecece;background: #fafafa;}
.uni-media-list-body{height: auto;justify-content: flex-start;}
.uni-media-list-text-top{font-size: 36upx;font-weight: 700;line-height: 60upx;}
.uni-media-list-logo{width: 210rpx;height: 290rpx;}
.uni-media-list-text-dec{font-size: 34rpx;
color: #659d0e;
width: 100%;
height: 75upx;
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
line-height: 75upx;
}
.uni-media-list-text-bottom{line-height: 60upx;}
</style>
