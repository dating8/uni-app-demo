<template>
	<view>
		<!-- 话题介绍 -->
		<topic-info :item="topicInfo"></topic-info>
		
		<swiper-tab-head
		:tabBars="tabBars" 
		:tabIndex="tabIndex" 
		@tabtap="tabtap" scrollStyle="border-bottom:0" scrollItemStyle="width:50%">
		</swiper-tab-head>
		<!-- 列表 -->
		<view class="toppic-detail-list">
			<block v-for="(item, index) in tablist" :key="index">
				<template v-if="tabIndex == index">
					<!-- 列表 -->
					<block v-for="(list,listIndex) in item.list" :key="listIndex">
						<commonList :item="list" :index="listIndex"></commonList>
					</block>
					<!-- 上拉加载 -->
					<load-more :loadtext="item.loadtext"></load-more>
				</template>
			</block>
		</view>
		
	</view>
</template>

<script>
	import topicInfo from "../../components/topic/topic-info.vue"
	import swiperTabHead from "../../components/index/swiper-tab-head.vue"
	import commonList from "../../components/common/common-list.vue"
	import loadMore from "../../components/common/load-more.vue"
	export default {
		components:{
			topicInfo,
			swiperTabHead,
			commonList,
			loadMore
		},
		data() {
			return {
				topicInfo:{
					titlepic:"../../static/demo/topicpic/13.jpeg",
					title:"忆往事，敬余生",
					desc:"我是描述",
					totalnum:1000,
					todaynum:1000,
				},
				tabIndex:0,
				tabBars: [{
				    name: '默认',
				    id: 'moren'
				}, {
					name: '最新',
					id: 'zuixin'
				}],
				tablist:[
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
		//监听用户下拉动作，一般用于下拉刷新
		onPullDownRefresh(){
			this.getData()
			
		},
		methods: {
			//上拉刷新
			getData(){
				//获取数据然后赋值之后关闭下拉刷新
				setTimeout(()=>{
					let arr = [
						// 文字
						{
							userpic: '../../static/demo/userpic/12.jpg',
							username: '哈哈1',
							sex: 0, //0男1女
							age: 25,
							isguanzhu: false,
							title: '我是标题1',
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
							username: '哈哈1',
							sex: 0, //0男1女
							age: 25,
							isguanzhu: false,
							title: '我是标题1',
							titlepic: '../../static/demo/datapic/13.jpg',
							video: false,
							share: false,
							path: '深圳 龙岗',
							sharenum: 20,
							commentnum: 30,
							goodnum: 40
						}
					]
					this.tablist[this.tabIndex].list = arr
					uni.stopPullDownRefresh()
				},2000)
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

</style>
