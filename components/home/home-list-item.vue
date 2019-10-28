<template>
	<view class="home-list-item u-f-ac u-f-jsb" hover-class="home-list-hover" @tap="clickevent">
		<view class="u-f-ac">
			<view class="icon iconfont" :class="['icon-'+item.icon]" v-if="item.icon"></view>{{item.name}}
		</view>
		<view class="icon iconfont icon-jinru"></view>
	</view>
</template>

<script>
	export default{
		props:{
			item:Object,
			index:Number
		},
		methods:{
			clickevent(){
				let item = this.item
				switch (item.clickType){
					case 'navigateTo':
					if(item.url){uni.navigateTo({url:item.url})}
						break;
					case 'redirectTo':
					if(item.url){uni.redirectTo({url:item.url})}
						break;
					case 'switchTab':
					if(item.url){uni.switchTab({url:item.url})}
						break;
					case 'clear':
					uni.showModal({
						title:'提示',
						content:'是否要清除缓存',
						confirmText:'立刻清除',
						success: (res) => {
							if(res.confirm){
								uni.clearStorage();
								un.uni.showToast({
									title: '清除缓存成功！'
								});
							}
						}
					})
						break;
				}
			}
		}
	}
</script>

<style scoped>
	.home-list-item{
		padding: 20upx;
		border-bottom: 1upx solid #f4f4f4;
	}
	.home-list-item>view:first-child{
		color: #333;
	}
	.home-list-item>view:first-child>view{
		margin-right: 10upx;
	}
	.home-list-item>view:last-child{
		color: #ccc;
	}
	.home-list-hover{
		background: #F4F4F4;
	}
</style>
