<template>
	<view class="user-space-head u-f-ajc">
		<image :src="getBgImg" mode="widthFix" lazy-load @tap="changeBgImg"></image>
		<view class="user-space-head-info u-f-ajc u-f-column">
			<image :src="userinfo.userpic" mode="widthFix" lazy-load></image>
			<view class="user-space-margin u-f-ac">
				{{userinfo.username}}<tag-sex-age :sex="userinfo.sex" :age="userinfo.age"></tag-sex-age>
			</view>
			<view class="icon iconfont user-space-head-btn user-space-margin" :class="[isguanzhu?'active':'icon-zengjia']" @tap="guanzhu">{{!isguanzhu?'关注':'已关注'}}</view>
		</view>
	</view>
</template>

<script>
	import tagSexAge from "../common/tag-sex-age.vue"
	export default {
		components:{
			tagSexAge
		},
		props:{
			userinfo:Object
		},
		data(){
			return{
				isguanzhu:this.userinfo.isguanzhu,
				bgimg:this.userinfo.bgimg,
			}
		},
		computed:{
			getBgImg(){
				return "../../static/bgimg/"+this.bgimg+".jpg"
			}
		},
		methods:{
			//切换背景
			changeBgImg(){
				let no = parseInt(this.bgimg);
				this.bgimg = no < 4 ? ++no : 1
			},
			//关注
			guanzhu(){
				this.isguanzhu = !this.isguanzhu
			}
		}
	}
</script>

<style scoped>
	.user-space-head{
		height: 500upx;
		position: relative;
		overflow: hidden;
	}
	.user-space-head>image{
		width: 100%;
	}
	.user-space-head-info{
		position: absolute;
		top: 150upx;
	}
	.user-space-head-info>image{
		width: 150upx;
		height: 150upx;
		border-radius: 100%;
	}
	.user-space-head-info>view:first-of-type{
		color: #FFFFFF;
		font-size: 35upx;
		font-weight: bold;
		text-shadow: 2upx 2upx 10upx #333333;
	}
	.user-space-head-btn{
		background: #FFE933;
		color: #333333;
		border: 1upx solid #FFE933;
		padding: 0 15upx;
		border-radius: 10upx;
		font-size: 28upx;
	}
	.user-space-head-btn.active{
		background: none;
		color: #fff;
		border: 1upx solid #FFFFFF;
	}
</style>
