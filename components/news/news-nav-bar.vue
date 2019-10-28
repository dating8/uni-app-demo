<template>
	<view>
		<uni-nav-bar :fixed="true" :statusBar="true" :border="false" @click-right="openAdd">
			<!-- 左边 -->
			<block slot="left">
				<view class="nav-left">
					<view class="icon iconfont icon-qiandao"></view>			
				</view>
			</block>
			<!-- 中间 -->
			<view class="nav-tab-bar u-f-ajc">
				<block v-for="(item, index) in tabBars" :key="item.id">
					<view class="u-f-ajc" :class="{'active':index == tabIndex}" @tap="changeTab(index)">
						{{item.name}}
						<view class="nav-tab-bar-line" v-if="tabIndex == index"></view>
					</view>
				</block>
			</view>
			<!-- 左边 -->
			<block slot="right">
				<view class="nav-right u-f-ajc">
					<view class="icon iconfont icon-bianji1"></view>			
				</view>
			</block>
		</uni-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue"
	export default {
		components:{
			uniNavBar
		},
		props:{
			tabBars: Array,
			tabIndex: Number
		},
		methods: {
			openAdd(){
				//打开发布页面
				uni.navigateTo({
					url:'../add-input/add-input'
				})
			},
			changeTab(index){
				this.$emit('change-tab', index)
			},
		}
	}
</script>

<style scoped>
	.nav-right>view,.nav-left>view{
		font-size: 40upx;
	}
	.nav-left{
		margin-left: 16upx;
	}
	.nav-right{
		width: 100%;
	}
	.nav-left>view{
		color: #ff9619;
	}
	.nav-tab-bar{
		width: 100%;
		margin-left: -20upx;
		position: relative;
	}
	.nav-tab-bar>view{
		font-size: 32upx;
		padding: 0 15upx;
		font-weight: bold;
		color: #969696;
	}
	.active{
		color: #333!important;
	}
	.nav-tab-bar-line{
		border-bottom: 5upx solid #ffde33;
		border-top: 5upx solid #ffde33;
		width: 70upx;
		border-radius: 20upx;
		position: absolute;
		bottom: 0upx;
	}
</style>
