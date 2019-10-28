<template>
	<view>
		<!-- 自定义导航栏 -->
		<uni-nav-bar :statusBar="true" rightText="发布" left-icon="arrowleft" @click-left="back" @click-right="submit">
			<view class="u-f-ajc" @tap="changelook">
				{{yinsi}}
				<view class="icon iconfont icon-xialazhankai"></view>
			</view>
		</uni-nav-bar>
		
		<view class="uni-textarea">
			<textarea v-model="text" placeholder="说一句话吧~" />
		</view>
		
		<upload-images @upload="upload"></upload-images>
		<uni-popup :show="showpopup" position="middle" mode="fixed" @hidePopup="hidePopup">
			<view class="gonggao">
				<view class="u-f-ajc">
					<image src="../../static/common/addinput.png" mode="widthFix"></image>
				</view>
				<view class="">
					1、涉及黄色，政治，广告及骚扰信息
				</view>
				<view class="">
					2、涉及人身攻击
				</view>
				<view class="">
					3、留联系方式，透露他人隐私
				</view>
				<view class="">
					一经核实将封禁，情节严重者永久封禁
				</view>
				<button type="default" @tap="hidePopup">朕知道了</button>
			</view>
		</uni-popup>
		
	</view>
</template>

<script>
	let changelook = ['所有人可见', '尽自己可见']
	import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue"
	import uniIcons from "../../components/uni-icons/uni-icons.vue"
	import uploadImages from "../../components/common/upload-images.vue"
	import uniPopup from '@/components/uni-popup/uni-popup.vue'
	export default {
		components:{
			uniNavBar,
			uniIcons,
			uploadImages,
			uniPopup
		},
		data() {
			return {
				yinsi:'所有人看见',
				text:'',
				imglist:[],
				showpopup:true,
				isget: false
			}
		},
		//监听页面返回
		onBackPress() {
			//如果有值
			if(!this.text && this.imglist.length < 1){
				return
			}
			if(!this.isget){
				this.baocun()
				return true
			}
		},
		methods: {
			//保存为草稿
			baocun(){
				uni.showModal({
					title: '提示',
					content: '是否保存为草稿',
					cancelText: '不保存',
					confirmText: '保存',
					success: (res) => {
						if (res.confirm) {
							console.log('保存');
						} else if (res.cancel) {
							console.log('不保存');
						}
						this.isget = true
						uni.navigateBack({
							delta: 1
						})
					}
				});
			},
			//返回
			back(){
				uni.navigateBack({
					delta: 1
				})
			},
			//发布
			submit(){
				console.log('发布')
			},
			changelook(){
				let _self = this
				uni.showActionSheet({
				    itemList: changelook,
				    success: (res) => {
						this.yinsi = changelook[res.tapIndex]
						console.log(this.yinsi)
				    }
				});
			},
			upload(arr){
				this.imglist = arr
			},
			hidePopup(){
				this.showpopup=false;
			}
		}
	}
</script>

<style>
	.uni-textarea{
		border: 1upx solid #eee;
	}
	.gonggao{
		width: 500upx;
	}
	.gonggao image{
		width: 75%;
		margin-bottom: 20upx;
	}
	.gonggao button{
		margin-top: 20upx;
		background: #FFE934;
		color: #171606;
	}
</style>
