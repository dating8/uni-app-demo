<template>
	<view>
		<!-- 操作菜单 -->
		<view class="paper-left-popup-mask" v-show="show" @tap="hidepopup"></view>
		<view class="paper-left-popup" v-show="show">
			<view class="u-f-ac" hover-class="paper-left-popup-h" @tap="addFriend">
				<view class="icon iconfont icon-sousuo"></view>
				加糗友
			</view>
			<view class="u-f-ac" hover-class="paper-left-popup-h" @tap="clear">
				<view class="icon iconfont icon-qingchu"></view>
				清除缓存
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			show:Boolean
		},
		methods:{
			//操作菜单
			addFriend(){
				this.$emit('addFriend')
			},
			clear(){
				this.$emit('clear')
			},
			hidepopup(){
				this.$emit('hidepopup')
			}
		}
	}
</script>

<style scoped>
	.paper-left-popup-mask{
		position: fixed;
		right: 0;
		top: 0;
		left: 0;
		bottom: 0;
		z-index: 100;
	}
	.paper-left-popup{
		position: fixed;
		right: 0;
		top: 10upx;
		background: #FFFFFF;
		z-index: 999;
		width: 55%;
		box-shadow: 1upx 1upx 2upx 2upx #CCCCCC;
	}
	.paper-left-popup>view{
		padding: 20upx;
		font-size: 35upx;
	}
	.paper-left-popup>view>view{
		margin-right: 10upx;
		font-weight: bold;
	}
	.paper-left-popup-h{
		background: #EEEEEE;
	}
</style>
