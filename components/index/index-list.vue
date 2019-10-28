<template>
	<view class="index-list animated fadeInLeft fast">
		<view class="index-list1 u-f-ac u-f-jsb">
			<view class="u-f-ac">
				<image :src="obj.userpic" 
				mode="widthFix" 
				lazy-load></image>
				{{obj.username}}
			</view>
			<view class="u-f-ac" v-show="!obj.isguanzhu" @tap="guanzhu">
				<view class="icon iconfont icon-zengjia"></view>关注
			</view>
		</view>
		<view class="index-list2" @tap="opendetail">{{obj.title}}</view>
		<view class="index-list3 u-f-ajc" @tap="opendetail">
			<!-- 图片 -->
			<image :src="obj.titlepic" 
			mode="widthFix" 
			lazy-load></image>
			<!-- 视频 -->
			<template v-if="obj.type=='video'">
				<view class="icon iconfont icon-bofang index-list-play"></view>
				<view class="index-list-playinfo">
					{{obj.playnum}}次播放 {{obj.long}}
				</view>
			</template>
		</view>
		<view class="index-list4 u-f-ac u-f-jsb">
			<view class="u-f-ac">
				<view class="u-f-ac" :class="{'active':(obj.infonum.index==1)}"
				@tap="caozuo('ding')">
					<view class="icon iconfont icon-icon_xiaolian-mian"></view>
					{{obj.infonum.dingnum}}
				</view>
				<view class="u-f-ac" :class="{'active':(obj.infonum.index==2)}"
				@tap="caozuo('cai')">
					<view class="icon iconfont icon-kulian"></view>
					{{obj.infonum.cainum}}
				</view>
			</view>
			<view class="u-f-ac">
				<view class="u-f-ac">
					<view class="icon iconfont icon-pinglun1"></view>
					{{obj.commentnum}}
				</view>
				<view class="u-f-ac">
					<view class="icon iconfont icon-zhuanfa"></view>
					{{obj.sharenum}}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return {
				obj:this.item
			}
		},
		props:{
			item:Object,
			index:Number
		},
		methods:{
			// 关注
			guanzhu(){
				uni.showToast({
					title: '关注成功',
				});
				this.obj.isguanzhu=true;
				// 通知父组件
				this.$emit('changeevent',this.obj,this.index);
				// 通知首页
				uni.$emit('updateData',this.obj,this.index);
			},
			// 顶踩
			caozuo(type){
				switch (type){
					case "ding":
					if(this.obj.infonum.index==1){ return; }
					this.obj.infonum.dingnum++;
					if(this.obj.infonum.index==2){
						this.obj.infonum.cainum--;
					}
					this.obj.infonum.index=1;
						break;
					case "cai":
					if(this.obj.infonum.index==2){ return; }
					this.obj.infonum.cainum++;
					if(this.obj.infonum.index==1){
						this.obj.infonum.dingnum--;
					}
					this.obj.infonum.index=2;
						break;
				}
			},
			// 进入详情页
			opendetail(){
				console.log("进入详情页")
				uni.navigateTo({
					url: '../../pages/detail/detail?detailData='+JSON.stringify(this.item)
				})
			}
		}
	}
</script>

<style scoped>
.index-list{
	padding: 20upx;
	border-bottom: 1upx solid #EEEEEE;
}
.index-list1>view:first-child{
	color: #999999;
}
.index-list1>view:first-child image{
	width: 85upx;
	height: 85upx;
	border-radius: 100%;
	margin-right: 10upx;
}
.index-list1>view:last-child{
	background: #F4F4F4;
	border-radius:5upx;
	padding: 0 10upx;
}
.index-list2{
	padding-top: 15upx;
	font-size: 32upx;
}
.index-list3{
	position: relative;
	padding-top: 15upx;
}
.index-list3>image{
	width: 100%;
	border-radius: 20upx;
}
.index-list4 view{
	color: #999999;
}
.index-list4{
	padding: 15upx 0;
}
.index-list4>view>view>view,.index-list4>view>view:first-child{
	margin-right: 10upx;
}
.index-list-play{
	position: absolute;
	font-size: 140upx;
	color: #FFFFFF;
}
.index-list-playinfo{
	position: absolute;
	background: rgba(51, 51, 51, 0.72);
	color: #FFFFFF;
	bottom: 8upx;
	right: 8upx;
	border-radius: 40upx;
	font-size: 22upx;
	padding: 0 12upx;
}
.index-list4 .active,.index-list4 .active>view{
	color: #C5F61C;
}
</style>
