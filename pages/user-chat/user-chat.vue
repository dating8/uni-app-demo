<template>
	<view>
		<scroll-view id="scrollview" scroll-y :scroll-top="scrollTop" :scroll-with-animation="true" :style="{height:style.contentH+'px'}">
			<!-- 聊天列表 -->
			<block v-for="(item,index) in list" :key="index">
				<!-- <user-chat-list :item="item" :index="index"></user-chat-list> -->
				<view class="user-chat-item">
					<view class="user-chat-time u-f-ajc" v-if="item.gstime">{{item.gstime}}</view>
					<view class="user-chat-list u-f" :class="{'user-chat-me':item.isme}">
						<image :src="item.userpic" mode="widthFix" lazy-load v-if="!item.isme"></image>
						<view class="user-chat-list-body">
							<!-- 文字 -->
							<text v-if="item.type === 'text'">{{item.data}}</text>
							<!-- 图片 -->
							<image :src="item.data" mode="widthFix" lazy-load v-if="item.type === 'img'"></image>
						</view>
						<image :src="item.userpic" mode="widthFix" lazy-load v-if="item.isme"></image>
					</view>
				</view>
			</block>
		</scroll-view>
		
		<!-- 输入框 -->
		<user-chat-bottom @submit="submit"></user-chat-bottom>
	</view>
</template>

<script>
	import userChatBottom from "../../components/user-chat/user-chat-bottom.vue"
	import time from "../../common/time.js"
	import userChatList from "../../components/user-chat/user-chat-list.vue"
	export default {
		components:{userChatBottom, userChatList},
		data() {
			return {
				scrollTop:0,
				style:{
					contentH:0,
					itemH:0
				},
				list:[]
			}
		},
		onLoad() {
			this.getData()
			this.initdata()
		},
		onReady() {
			this.pageToBottom()
		},
		methods: {
			//初始化参数
			initdata(){
				try{
					const res = uni.getSystemInfoSync();
					this.style.contentH = res.windowHeight - uni.upx2px(120);
				}catch(e){}
			},
			pageToBottom(){
				const query = uni.createSelectorQuery().in(this);
				query.select('#scrollview').boundingClientRect();
				query.selectAll('.user-chat-item').boundingClientRect();
				query.exec((res) => {
					res[1].forEach(ret => {
						this.style.itemH += ret.height
					})
					if(this.style.itemH > this.style.contentH){
						this.scrollTop = this.style.itemH
					}
				})
			},
			//获取聊天数据
			getData(){
				let arr =[
					{
						userpic:'../../static/demo/userpic/11.jpg',
						isme:false,
						type:'text',
						data:'哈哈哈',
						time:'1555146414'
					},
					{
						userpic:'../../static/demo/userpic/6.jpg',
						isme:true,
						type:'img',
						data:'../../static/demo/3.jpg',
						time:'1572242718'
					},
				];
				for(let i = 0; i<arr.length;i++){
					arr[i].gstime = time.gettime.getChatTime(arr[i].time,i>0?arr[i-1].time:0)
				}
				this.list = arr
			},
			submit(data){
				//构建数据
				let now = new Date().getTime()
				let obj = {
						userpic:'../../static/demo/userpic/6.jpg',
						isme:true,
						type:'text',
						data:data,
						time:now,
						gstime:time.gettime.getChatTime(now,this.list[this.list.length - 1].time)
					}
				this.list.push(obj)
				this.pageToBottom()
			}
		}
	}
</script>

<style>
.user-chat-list{
		padding: 20upx 0;
	}
	.user-chat-list>image{
		width: 100upx;
		height: 100upx;
		border-radius: 100%;
		flex-shrink: 0;
	}
	.user-chat-list-body{
		position: relative;
		background: #F4F4F4;
		padding: 25upx;
		margin-left: 20upx;
		margin-right: 100upx;
		border-radius: 20upx;
	}
	.user-chat-list-body:after{
		position: absolute;
		left: -30upx;
		right: 0;
		top: 30upx;
		content: '';
		width: 0;
		height: 0;
		border: 16upx solid #f4f4f4;
		border-color: transparent #f4f4f4 transparent transparent;
	}
	.user-chat-me{
		justify-content: flex-end;
	}
	.user-chat-me .user-chat-list-body{
		margin-left: 100upx;
		margin-right: 20upx;
	}
	.user-chat-me .user-chat-list-body:after{
		right: -30upx;
		left: auto;
		border-color: transparent transparent transparent #f4f4f4;
	}
	.user-chat-list-body>image{
		max-width: 150upx;
		max-height: 200upx;
	}
	.user-chat-time{
		padding: 50upx 0;
		color: #a2a2a2;
		font-size: 24upx;
	}
</style>
