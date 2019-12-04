<template>
	<view>
		
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

</style>
