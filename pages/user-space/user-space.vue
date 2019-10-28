<template>
	<view>
		<!-- 背景图 -->
		<user-space-head :userinfo="userinfo"></user-space-head>
		<!-- 统计 -->
		<view class="user-space-data">
			<home-data :homedata="spacedata"></home-data>
		</view>
		<view style="height: 20upx;background: #F4F4F4;"></view>
		<!-- tab导航 -->
		<swiper-tab-head
		:tabBars="tabBars" 
		:tabIndex="tabIndex" 
		@tabtap="tabtap" scrollStyle="border-bottom:0" scrollItemStyle="width:33.33%">
		</swiper-tab-head>
		
		
		
		
		<block v-for="(item, index) in tablist" :key="index">
			<template v-if="tabIndex == 0">
				<!-- 主页 -->
				<user-space-userinfo :userinfo="userinfo"></user-space-userinfo>
			</template>
			<template v-else-if="tabIndex == index">
				<!-- 列表 -->
				<block v-for="(list,listIndex) in item.list" :key="listIndex">
					<commonList :item="list" :index="listIndex"></commonList>
				</block>
				<!-- 上拉加载 -->
				<load-more :loadtext="item.loadtext"></load-more>
			</template>
		</block>
		
		<!-- 操作菜单 -->
		<user-space-popup :show="show" 
		@lahei="lahei" @beizhu="beizhu" @hidepopup="hidepopup"></user-space-popup>
	</view>
</template>

<script>
	import userSpaceHead from "../../components/user-space/user-space-head.vue"
	import homeData from "../../components/home/home-data.vue"
	import swiperTabHead from "../../components/index/swiper-tab-head.vue"
	import userSpaceUserinfo from "../../components/user-space/user-space-userinfo.vue"
	import commonList from "../../components/common/common-list.vue"
	import loadMore from "../../components/common/load-more.vue"
	import userSpacePopup from "../../components/user-space/user-space-popup.vue"
	export default {
		components:{userSpaceHead, homeData, swiperTabHead,userSpaceUserinfo, commonList, loadMore, userSpacePopup},
		data() {
			return {
				show:false,
				userinfo:{
					bgimg:1,
					userpic:'../../static/demo/userpic/14.jpg',
					username:'小不点',
					sex:0,
					age:20,
					isguanzhu:false,
					regtime:'2019-04-11',
					id:'123456',
					birthday:'2008-08-08',
					job:'IT',
					qg:'未婚',
					path:"广东广州"
				},
				spacedata:[
					{name:'获赞',num:"10k"},
					{name:'关注',num:11},
					{name:'评论',num:20}
				],
				tabIndex:0,
				tabBars: [{
				    name: '主页',
				    id: 'zhuye'
				}, {
					name: '糗事',
					id: 'qiushi'
				}, {
					name: '动态',
					id: 'dongtai'
				}],
				tablist:[{},
					{
						loadtext: '上拉加载更多',
						list:[
							// 文字
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 0, //0男1女
								age: 25,
								isguanzhu: false,
								title: '我是标题',
								titlepic: '',
								video: false,
								share: false,
								path: '深圳 龙岗',
								sharenum: 20,
								commentnum: 30,
								goodnum: 40
							},
							// 图文
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 0, //0男1女
								age: 25,
								isguanzhu: false,
								title: '我是标题',
								titlepic: '../../static/demo/datapic/13.jpg',
								video: false,
								share: false,
								path: '深圳 龙岗',
								sharenum: 20,
								commentnum: 30,
								goodnum: 40
							},
							// 视频
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 1, //0男1女
								age: 25,
								isguanzhu: false,
								title: '我是标题',
								titlepic: '../../static/demo/datapic/13.jpg',
								video: {
									looknum: '20w',
									long: '2:17'
								},
								share: false,
								path: '深圳 龙岗',
								sharenum: 20,
								commentnum: 30,
								goodnum: 40
							},
							// 分享
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 0, //0男1女
								age: 25,
								isguanzhu: false,
								title: '我是标题',
								titlepic: '',
								video: false,
								share: {
									title:'我是分享标题',
									titlepic: '../../static/demo/datapic/14.jpg'
								},
								path: '深圳 龙岗',
								sharenum: 20,
								commentnum: 30,
								goodnum: 40
							}
						]
					},
					{
						loadtext: '上拉加载更多',
						list:[
							// 文字
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 0, //0男1女
								age: 25,
								isguanzhu: false,
								title: '我是标题',
								titlepic: '',
								video: false,
								share: false,
								path: '深圳 龙岗',
								sharenum: 20,
								commentnum: 30,
								goodnum: 40
							},
							// 图文
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 0, //0男1女
								age: 25,
								isguanzhu: false,
								title: '我是标题',
								titlepic: '../../static/demo/datapic/13.jpg',
								video: false,
								share: false,
								path: '深圳 龙岗',
								sharenum: 20,
								commentnum: 30,
								goodnum: 40
							}
						]
					}
				]
			}
		},
		//上拉触底事件
		onReachBottom() {
			this.loadmore()
		},
		onNavigationBarButtonTap(e){
			if(e.index == 0){
				this.hidepopup()
			}
		},
		methods: {
			//操作菜单显示隐藏
			hidepopup(){
				this.show = !this.show
			},
			//拉黑
			lahei(){
				console.log('拉黑')
				this.hidepopup()
			},
			//备注
			beizhu(){
				console.log('beizhu')
				this.hidepopup()
			},
			//tabbar点击事件
			tabtap(index){
				this.tabIndex = index
			},
			//上拉加载
			loadmore(){
				if(this.tablist[this.tabIndex].loadtext != '上拉加载更多'){return}
				// 修改状态
				this.tablist[this.tabIndex].loadtext="加载中...";
				// 获取数据
				setTimeout(() => {
					//获取完成
					let obj = {
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 0, //0男1女
								age: 25,
								isguanzhu: false,
								title: '我是标题',
								titlepic: '../../static/demo/datapic/13.jpg',
								video: false,
								share: false,
								path: '深圳 龙岗',
								sharenum: 20,
								commentnum: 30,
								goodnum: 40
							}
					this.tablist[this.tabIndex].list.push(obj)
					this.tablist[this.tabIndex].loadtext = '上拉加载更多'
				},1000)
			}
		}
	}
</script>

<style>
.user-space-margin{
	margin: 15upx 0;
}
.user-space-data{
	background: #FFFFFF;
	position: relative;
	z-index: 10;
	border-radius: 20upx 20upx 0 0;
	margin-top: -15upx;
}

</style>
