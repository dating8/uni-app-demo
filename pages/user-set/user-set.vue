<template>
	<view class="body">
		<block v-for="(item,index) in list" :key="index">
			<home-list-item :item="item" :index="index"></home-list-item>
		</block>
		<button type="primary" class="user-set-btn">退出登录</button>
	</view>
</template>

<script>
	import homeListItem from "../../components/home/home-list-item.vue"
	export default {
		components:{homeListItem},
		data() {
			return {
				list:[
					{name:'账号与安全',clickType:'navigateTo',url:'../../pages/user-set-password/user-set-password'},
					{name:'绑定邮箱',clickType:'navigateTo',url:'../../pages/user-set-email/user-set-email'},
					{name:'资料编辑',clickType:'navigateTo',url:'../../pages/user-set-userinfo/user-set-userinfo'},
					{name:'小纸条',clickType:'',url:''},
					{name:'清除缓存',clickType:'clear',url:''},
					{name:'意见反馈',clickType:'navigateTo',url:'../../pages/user-set-help/user-set-help'},
					{name:'关于糗百',clickType:'navigateTo',url:'../../pages/user-set-about/user-set-about'}
				],
			}
		},
		methods: {
			
		}
	}
</script>

<style>
@import "../../common/form.css";
</style>
