<template>
	<view>
		<swiper-tab-head
		:tabBars="tabBars" 
		:tabIndex="tabIndex" 
		@tabtap="tabtap">
		</swiper-tab-head>
		
		<view class="uni-tab-bar">
			<swiper class="swiper-box" 
			:style="{height:swiperHeight+'px'}" 
			:current="tabIndex" 
			@change="ontabchange">
				<swiper-item v-for="(items,index) in newslist" :key="index">
					<scroll-view scroll-y class="list" @scrolltolower="loadmore(index)">
						<template v-if="items.list.length > 0">
							<block v-for="(item,index1) in items.list" :key="index1">
								<view class="topic-view">
									<topic-list :item="item" :index="index1"></topic-list>
								</view>
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
	import topicList from "../../components/news/topic-list.vue"
	import loadMore from "../../components/common/load-more.vue"
	import noThing from "../../components/common/no-thing.vue"
	export default {
		components:{
			swiperTabHead,
			loadMore,
			noThing,
			topicList
		},
		data() {
			return {
				swiperHeight:500,
				tabIndex:0,
				tabBars: [{
				    name: '关注',
				    id: 'guanzhu'
				}, {
					name: '推荐',
					id: 'tuijian'
				}, {
					name: '体育',
					id: 'tiyu'
				}, {
					name: '热点',
					id: 'redian'
				}, {
					name: '财经',
					id: 'caijing'
				}, {
					name: '娱乐',
					id: 'yule'
				}],
				newslist:[
					{
						loadtext:"上拉加载更多",
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
							},
							{
								titlepic:'../../static/demo/topicpic/13.jpeg',
								title:'话题名称',
								desc:'我是话题名称描述',
								totalnum:50,
								todaynum:10
							}
						]
					},
					{
						loadtext:"上拉加载更多",
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
					},
					{
						loadtext:"上拉加载更多",
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
							},
							{
								titlepic:'../../static/demo/topicpic/13.jpeg',
								title:'话题名称',
								desc:'我是话题名称描述',
								totalnum:50,
								todaynum:10
							}
						]
					},
					{
						loadtext:"上拉加载更多",
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
							},
							{
								titlepic:'../../static/demo/topicpic/13.jpeg',
								title:'话题名称',
								desc:'我是话题名称描述',
								totalnum:50,
								todaynum:10
							}
						]
					},{
						loadtext:"上拉加载更多",
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
							}
						]
					},{
						loadtext:"上拉加载更多",
						list:[]
					}
				]
			}
		},
		methods: {
			//上拉加载
			loadmore(index){
				if(this.newslist[index].loadtext != '上拉加载更多'){return}
				// 修改状态
				this.newslist[index].loadtext="加载中...";
				// 获取数据
				setTimeout(() => {
					//获取完成
					let obj = {
							titlepic:'../../static/demo/topicpic/13.jpeg',
							title:'话题名称',
							desc:'我是话题名称描述',
							totalnum:50,
							todaynum:10
						}
					this.newslist[index].list.push(obj)
					this.newslist[index].loadtext = '上拉加载更多'
				},2000)
				
				// this.newslist[index].loadtext = '没有更多数据了'
			},
			//tabbar点击事件
			tabtap(index){
				this.tabIndex = index
			},
			//滑动事件
			ontabchange(e){
				this.tabIndex = e.detail.current
			}
		}
	}
</script>
	
<style>
.topic-view{
	padding: 0 20upx;
}
</style>
