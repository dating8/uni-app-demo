<template>
	<view class="tag-sex icon iconfont" :class="[sex == 0?'icon-nan':'icon-nv']">{{age}}</view>
</template>

<script>
	export default {
		props:{
			age:Number,
			sex:Number
		}
	}
</script>

<style scoped>
	.tag-sex{
		line-height: 26upx;
		background: #007AFF;
		color: #fff;
		font-size: 23upx;
		padding: 5upx 10upx;
		margin-left: 10upx;
		border-radius: 22upx;
	}
	.icon-nv{
		background: #ff698d;
	}
</style>
