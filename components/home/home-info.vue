<template>
	<view class="home-info u-f-ac" @tap="toUerSpace">
		<image :src="item.userpic" mode="widthFix" lazy-load></image>
		<view class="u-f1">
			<view>{{item.username}}</view>
			<view>总访客 {{item.totalnum}} 今日 {{item.todaynum}}</view>
		</view>
		<view class="icon iconfont icon-jinru"></view>
	</view>
</template>

<script>
	export default {
		props:{
			item:Object
		},
		methods:{
			toUerSpace(){
				uni.navigateTo({
					url:'../../pages/user-space/user-space'
				})
			}
		}
	}
</script>

<style scoped>
	.home-info{
		padding: 20upx 40upx;
	}
	.home-info>image{
		flex-shrink: 0;
		width: 100upx;
		height: 100upx;
		border-radius: 100%;
		margin-right: 15upx;
	}
	.home-info>view:first-of-type>view:first-child{
		font-size: 32upx;
	}
	.home-info>view:first-of-type>view:last-child{
		font-size: #bbbbbb;
	}
	.home-info>view:last-of-type{
		height: 100%;
	}
</style>
