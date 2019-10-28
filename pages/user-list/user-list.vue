<template>
	<view class="body">
		<!-- tab切换 -->
		<swiper-tab-head
		:tabBars="tabBars" 
		:tabIndex="tabIndex" 
		@tabtap="tabtap" scrollStyle="border-bottom:0" scrollItemStyle="width:33%">
		</swiper-tab-head>
		
		<!-- 好友列表 -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box" 
			:style="{height:swiperHeight+'px'}" 
			:current="tabIndex" 
			@change="ontabchange">
				<swiper-item v-for="(items,index) in newslist" :key="index">
					<scroll-view scroll-y class="list" @scrolltolower="loadmore(index)">
						<template v-if="items.list.length > 0">
							<block v-for="(item,index1) in items.list" :key="index1">
								<user-list :item="item" :index="index1"></user-list>
							</block>
							<!-- 上拉加载 -->
							<load-more :loadtext="items.loadtext"></load-more>
						</template>
						
						<template v-else>
							<no-thing></no-thing>
						</template>
						
						
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
		
	</view>
</template>

<script>
	import swiperTabHead from "../../components/index/swiper-tab-head.vue"
	import userList from "../../components/user-list/user-list.vue"
	import loadMore from "../../components/common/load-more.vue"
	import noThing from "../../components/common/no-thing.vue"
	export default {
		components:{
			swiperTabHead,
			userList,
			loadMore,
			noThing
		},
		data() {
			return {
				swiperHeight:0,
				tabIndex:0,
				tabBars: [{
				    name: '互关',
				    id: 'huguan',
					num: 10
				}, {
					name: '关注',
					id: 'guanzhu',
					num: 20
				}, {
					name: '粉丝',
					id: 'fensi',
					num: 30
				}],
				newslist:[
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic: '../../static/demo/userpic/11.jpg',
								username: '哈哈',
								sex: 0, //0男1女
								age: 25,
								isguanzhu: true,
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 1, //0男1女
								age: 20,
								isguanzhu: false,
							},
							{
								userpic: '../../static/demo/userpic/11.jpg',
								username: '哈哈',
								sex: 0, //0男1女
								age: 25,
								isguanzhu: true,
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 1, //0男1女
								age: 20,
								isguanzhu: false,
							},
							{
								userpic: '../../static/demo/userpic/11.jpg',
								username: '哈哈',
								sex: 0, //0男1女
								age: 25,
								isguanzhu: true,
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 1, //0男1女
								age: 20,
								isguanzhu: false,
							},
							{
								userpic: '../../static/demo/userpic/11.jpg',
								username: '哈哈',
								sex: 0, //0男1女
								age: 25,
								isguanzhu: true,
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 1, //0男1女
								age: 20,
								isguanzhu: false,
							}
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic: '../../static/demo/userpic/11.jpg',
								username: '哈哈',
								sex: 1, //0男1女
								age: 25,
								isguanzhu: true,
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 0, //0男1女
								age: 20,
								isguanzhu: false,
							}
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic: '../../static/demo/userpic/11.jpg',
								username: '哈哈',
								sex: 0, //0男1女
								age: 25,
								isguanzhu: true,
							},
							{
								userpic: '../../static/demo/userpic/12.jpg',
								username: '哈哈',
								sex: 1, //0男1女
								age: 20,
								isguanzhu: false,
							}
						]
					}
				]
				
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
			//监听原生标题栏按钮点击事件
			onNavigationBarButtonTap(e){
				if(e.index == 0){
					//点击第一个按钮，也就是取消按钮
					uni.navigateBack({
						delta:1
					})
				}
			},
			//监听原生标题栏搜索输入框输入内容变化事件
			onNavigationBarSearchInputChanged(e){
				console.log(e.text)
			},
			//监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。
			onNavigationBarSearchInputConfirmed(e){
				console.log(e.text)
			},
			//tabbar点击事件
			tabtap(index){
				this.tabIndex = index
			},
			//滑动事件
			ontabchange(e){
				this.tabIndex = e.detail.current
			},
			//上拉加载
			loadmore(index){
				if(this.newslist[index].loadtext != '上拉加载更多'){return}
				// 修改状态
				this.newslist[index].loadtext="加载中...";
				// 获取数据
				setTimeout(() => {
					//获取完成
					let obj = {
								userpic: '../../static/demo/userpic/11.jpg',
								username: '哈哈加载',
								sex: 0, //0男1女
								age: 25,
								isguanzhu: true,
							}
					this.newslist[index].list.push(obj)
					this.newslist[index].loadtext = '上拉加载更多'
				},2000)
				
				// this.newslist[index].loadtext = '没有更多数据了'
			}
		}
	}
</script>

<style>
</style>
