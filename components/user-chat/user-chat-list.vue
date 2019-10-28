<template>
	<view class="user-chat-item">
		<view class="user-chat-time u-f-ajc" v-if="item.gstime">{{item.gstime}}</view>
		<view class="user-chat-list u-f" :class="{'user-chat-me':item.isme}">
			<image :src="item.userpic" mode="widthFix" lazy-load v-if="!item.isme"></image>
			<view class="user-chat-list-body">
				<!-- 文字 -->
				<text v-if="item.type === 'text'">{{item.data}}</text>
				<!-- 图片 -->
				<image :src="item.data" mode="widthFix" lazy-load v-if="item.type === 'img'"></image>
			</view>
			<image :src="item.userpic" mode="widthFix" lazy-load v-if="item.isme"></image>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			item:Object,
			index:Number
		}
	}
</script>

<style scoped>
	.user-chat-list{
		padding: 20upx 0;
	}
	.user-chat-list>image{
		width: 100upx;
		height: 100upx;
		border-radius: 100%;
		flex-shrink: 0;
	}
	.user-chat-list-body{
		position: relative;
		background: #F4F4F4;
		padding: 25upx;
		margin-left: 20upx;
		margin-right: 100upx;
		border-radius: 20upx;
	}
	.user-chat-list-body:after{
		position: absolute;
		left: -30upx;
		right: 0;
		top: 30upx;
		content: '';
		width: 0;
		height: 0;
		border: 16upx solid #f4f4f4;
		border-color: transparent #f4f4f4 transparent transparent;
	}
	.user-chat-me{
		justify-content: flex-end;
	}
	.user-chat-me .user-chat-list-body{
		margin-left: 100upx;
		margin-right: 20upx;
	}
	.user-chat-me .user-chat-list-body:after{
		right: -30upx;
		left: auto;
		border-color: transparent transparent transparent #f4f4f4;
	}
	.user-chat-list-body>image{
		max-width: 150upx;
		max-height: 200upx;
	}
	.user-chat-time{
		padding: 50upx 0;
		color: #a2a2a2;
		font-size: 24upx;
	}
</style>
