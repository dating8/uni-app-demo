<template>
	<view class="body">
		<paper-left-popup :show="show" @addFriend="addFriend" @clear="clear" @hidepopup="hidepopup"></paper-left-popup>
		<!-- 小纸条列表 -->
		<block v-for="(item,index) in list" :key="index">
			<paper-list :item="item" :index="index"></paper-list>
		</block>
		<!-- 上拉加载 -->
		<load-more :loadtext="loadtext"></load-more>
	</view>
</template>

<script>
	import paperList from "../../components/paper/paper-list.vue"
	import loadMore from "../../components/common/load-more.vue"
	import paperLeftPopup from "../../components/paper/paper-left-popup.vue"
	export default {
		components: {
			paperList,
			loadMore,
			paperLeftPopup
		},
		data() {
			return {
				show: false,
				loadtext: '上拉加载更多',
				list: [
					{
						userpic:'../../static/demo/userpic/12.jpg',
						username:'昵称',
						time:'10:21',
						data:'我是信息',
						noreadnum:2
					},
					{
						userpic:'../../static/demo/userpic/12.jpg',
						username:'昵称',
						time:'10:21',
						data:'我是信息',
						noreadnum:2
					},
					{
						userpic:'../../static/demo/userpic/12.jpg',
						username:'昵称',
						time:'10:21',
						data:'我是信息',
						noreadnum:2
					},
					{
						userpic:'../../static/demo/userpic/12.jpg',
						username:'昵称',
						time:'10:21',
						data:'我是信息',
						noreadnum:2
					},
					{
						userpic:'../../static/demo/userpic/12.jpg',
						username:'昵称',
						time:'10:21',
						data:'我是信息',
						noreadnum:2
					},
					{
						userpic:'../../static/demo/userpic/12.jpg',
						username:'昵称',
						time:'10:21',
						data:'我是信息',
						noreadnum:2
					},
					{
						userpic:'../../static/demo/userpic/12.jpg',
						username:'昵称',
						time:'10:21',
						data:'我是信息',
						noreadnum:2
					}
				]
			}
		},
		//监听用户下拉动作，一般用于下拉刷新
		onPullDownRefresh(){
			this.getData()
			
		},
		//上拉触底事件
		onReachBottom() {
			this.loadmore()
		},
		//监听导航按钮点击事件
		onNavigationBarButtonTap(e) {
			switch (e.index){
				case 0:
				uni.navigateTo({
					url: '../user-list/user-list'
				});
				this.hidepopup()
					break;
				case 1:
				this.showpopup()
					break;
			}
		},
		methods: {
			//操作菜单
			addFriend(){
				this.hidepopup()
			},
			clear(){
				this.hidepopup()
			},
			hidepopup(){
				this.show = false
			},
			showpopup(){
				this.show = true
			},
			//上拉加载
			loadmore(){
				if(this.loadtext != '上拉加载更多'){return}
				// 修改状态
				this.loadtext="加载中...";
				// 获取数据
				setTimeout(() => {
					//获取完成
					let obj = {
						userpic:'../../static/demo/userpic/12.jpg',
						username:'昵称',
						time:'10:21',
						data:'我是信息888',
						noreadnum:0
					}
					this.list.push(obj)
					this.loadtext = '上拉加载更多'
				},1000)
			},
			//上拉刷新
			getData(){
				//获取数据然后赋值之后关闭下拉刷新
				setTimeout(()=>{
					let arr = [
						{
							userpic:'../../static/demo/userpic/12.jpg',
							username:'昵称1',
							time:'10:21',
							data:'我是信息1',
							noreadnum:3
						},
						{
							userpic:'../../static/demo/userpic/12.jpg',
							username:'昵称1',
							time:'10:21',
							data:'我是信息1',
							noreadnum:3
						}
					]
					this.list = arr
					uni.stopPullDownRefresh()
				},2000)
			},
		}
	}
</script>

<style>
.body{
	padding: 0 20upx;
}

</style>
