<template>
	<view>
		<template v-if="!isLogin">
			<!-- 未登录 -->
			<view class="u-f-ajc">登录仿糗百，体验更多功能</view>
			<!-- 第三方登录 -->
			<other-login></other-login>
			<!-- 账号密码登录 -->
			<view class="u-f-ajc" @tap="openLogin">账号密码登录<view class="icon iconfont icon-jinru"></view></view>
		</template>
		<template v-else>
			<!-- 已登录 -->
			<home-info :item="homeinfo"></home-info>
		</template>
		
		<!-- 数据 -->
		<home-data :homedata="homedata"></home-data>
		<!-- 广告位 -->
		<view class="home-adv u-f-ajc">
			<image src="../../static/demo/demo20.jpg" mode="widthFix" lazy-load></image>
		</view>
		
		<!-- 功能列表 -->
		<view class="home-list">
			<block v-for="(item,index) in list" :key="index">
				<home-list-item :item="item" :index="index"></home-list-item>
			</block>
		</view>
	</view>
</template>

<script>
	import homeListItem from "../../components/home/home-list-item.vue"
	import homeInfo from "../../components/home/home-info.vue"
	import otherLogin from "../../components/home/other-login.vue"
	import homeData from "../../components/home/home-data.vue"
	export default {
		components:{homeListItem, homeInfo, otherLogin ,homeData},
		data() {
			return {
				isLogin: true,
				homeinfo:{
					userpic:'../../static/demo/userpic/11.jpg',
					username:'',
					totalnum:0,
					todaynum:0
				},
				list:[
					{name:'浏览历史',icon:'liulan',clickType:'',url:''},
					{name:'糗百认证',icon:'huiyuanvip',clickType:'',url:''},
					{name:'审核糗事',icon:'keyboard',clickType:'',url:''}
				],
				homedata:[
					{name:'糗事',num:0},
					{name:'动态',num:0},
					{name:'评论',num:0},
					{name:'收藏',num:0}
				]
			}
		},
		onNavigationBarButtonTap(e) {
			if(e.index == 0){
				uni.navigateTo({
					url: '../user-set/user-set'
				})
			}
		},
		methods: {
			openLogin(){
				uni.navigateTo({
					url:'../login/login'
				})
			}
		}
	}
</script>

<style>


.home-adv{
	padding: 20upx;
}
.home-adv image{
	height: 170upx;
	border-radius: 20upx;
}
.home-list{
	padding: 20upx;
}
</style>
