<template>
	<view>
		<!-- 自定义导航栏 -->
		<news-nav-bar 
		:tabBars="tabBars" 
		:tabIndex="tabIndex" 
		@change-tab="changeTab">
		</news-nav-bar>
		<!-- 列表 -->
		
		<view class="uni-tab-bar">
			<swiper class="swiper-box" 
			:style="{height:swiperHeight+'px'}" 
			:current="tabIndex" 
			@change="ontabchange">
				<!-- 关注 -->
				<swiper-item>
					<scroll-view scroll-y class="list" @scrolltolower="loadmore()">
						<template v-if="guanzhu.list.length > 0">
							<block v-for="(item, index) in guanzhu.list" :key="index">
								<commonList :item="item" :index="index"></commonList>
							</block>
							<!-- 上拉加载 -->
							<load-more :loadtext="guanzhu.loadtext"></load-more>
						</template>
						
						<template v-else>
							<no-thing></no-thing>
						</template>
						
					</scroll-view>
				</swiper-item>
				<!-- 话题 -->
				<swiper-item>
					<scroll-view scroll-y class="list">
						<!-- 搜索框 -->
						<view class="search-input">
							<input class="uni-input" placeholder="搜索内容" placeholder-class="icon iconfont icon-sousuo topic-search" />
						</view>
						
						<!-- 轮播图 -->
						<swiper class="topic-swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
							<block v-for="(item, index) in huati.swiper" :key="index">
								<swiper-item>
									<image :src="item.src" mode="widthFix" lazy-load></image>
								</swiper-item>
							</block>
		
						</swiper>
						<!-- 热门分类 -->
						<topic-nav :nav="huati.nav"></topic-nav>
						<!-- 最近更新 -->
						<view class="topic-new">
							<view class="">最近更新</view>
							<block v-for="(item, index) in huati.list" :key="index">
								<topic-list :item="item" :index="index"></topic-list>
							</block>
						</view>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
		
	</view>
</template>

<script>
	import newsNavBar from "../../components/news/news-nav-bar.vue"
	import commonList from "../../components/common/common-list.vue"
	import loadMore from "../../components/common/load-more.vue"
	import noThing from "../../components/common/no-thing.vue"
	import topicNav from "../../components/news/topic-nav.vue"
	import topicList from "../../components/news/topic-list.vue"
	export default {
		components:{
			newsNavBar,
			commonList,
			loadMore,
			noThing,
			topicNav,
			topicList
		},
		data() {
			return {
				swiperHeight:0,
				tabIndex: 0,
				tabBars: [
					{name: '关注', id: 'guanzhu'},
					{name: '话题', id: '话题'}
				],
				guanzhu:{
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
						// 视频
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
				huati:{
					swiper:[
						{src:'../../static/demo/banner1.jpg'},
						{src:'../../static/demo/banner2.jpg'},
						{src:'../../static/demo/banner1.jpg'}
					],
					nav:[
						{name: '最新'},
						{name: '游戏'},
						{name: '打卡'},
						{name: '情感'},
						{name: '故事'},
						{name: '喜爱'}
					],
					list:[
						{
							titlepic:'../../static/demo/topicpic/13.jpeg',
							title:'话题名称',
							desc:'我是话题名称描述',
							totalnum:50,
							todaynum:10
						},
						{
							titlepic:'../../static/demo/topicpic/13.jpeg',
							title:'话题名称',
							desc:'我是话题名称描述',
							totalnum:50,
							todaynum:10
						},
						{
							titlepic:'../../static/demo/topicpic/13.jpeg',
							title:'话题名称',
							desc:'我是话题名称描述',
							totalnum:50,
							todaynum:10
						}
					]
				}
			}
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res) => {
					let height = res.windowHeight-uni.upx2px(100);//100是上面导航栏.uni-tab-bar的高度
					this.swiperHeight = height
				}
			})
		},
		methods: {
			//点击切换
			changeTab(index){
				this.tabIndex = index
			},
			//滑动事件
			ontabchange(e){
				this.tabIndex = e.detail.current
			},
			//上拉加载
			loadmore(index){
				if(this.guanzhu.loadtext != '上拉加载更多'){return}
				// 修改状态
				this.guanzhu.loadtext="加载中...";
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
					this.guanzhu.list.push(obj)
					this.guanzhu.loadtext = '上拉加载更多'
				},1000)
			}
		}
	}
</script>

<style>
.topic-swiper{
	padding: 0 20upx 20upx 20upx;
}
.topic-swiper image{
	width: 100%;
	border-radius: 10upx;
}
.search-input{
	padding: 20upx;
}
.search-input>input{
	background: #F4F4F4;
	border-radius:10upx;
}
.topic-search{
	display: flex;
	justify-content: center;
	font-size: 28upx;
}

.topic-new{
	padding: 20upx;
}
.topic-new>view:first-child{
	padding-bottom: 5upx;
	font-size: 32upx;
}
</style>
