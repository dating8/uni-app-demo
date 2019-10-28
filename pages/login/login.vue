<template>
	<view>
		<!-- 状态栏 -->
		<uni-status-bar bgColor="#ffe933"/>
		<view class="icon iconfont icon-guanbi" @tap="back"></view>
		<!-- 登录 -->
		<image src="../../static/common/loginhead.png" mode="widthFix" lazy-load class="loginhead"></image>
		<!-- 输入框 -->
		<view class="body">
			<!-- 账号密码登录 -->
			<template v-if="!status">
				<input type="text" v-model="username"
				class="uni-input common-input" 
				placeholder="昵称/手机号/邮箱" />
				
				<view class="login-input-box">
					<input type="text" password v-model="password"
					class="uni-input common-input forget-input" 
					placeholder="请输入密码" />
					<view class="forget u-f-ajc login-font-color">忘记密码</view>
				</view>
			</template>
			
			<!-- 验证码登录方式 -->
			<template v-if="status">
				<view class="login-input-box">
					<view class="phone u-f-ajc">+86</view>
					<input type="text" v-model="phone"
					class="uni-input common-input phone-input" 
					placeholder="手机号" />
				</view>
				<view class="login-input-box">
					<input type="text" v-model="checknum"
					class="uni-input common-input forget-input" 
					placeholder="请输入验证码" />
					<view class="forget u-f-ajc login-font-color yanzhenma" @tap="getCheckNum">
						<view class="u-f-ajc">{{!codetime?'获取验证码':codetime}}</view>
					</view>
				</view>
			</template>
			
			<button class="user-set-btn" 
			:loading="loading" :class="{'user-set-btn-disable':disabled}" 
			type="primary" @tap="submit" :disabled="disabled">登录</button>
		</view>
		<!-- 登录状态切换 -->
		<view class="login-status login-padding login-font-color u-f-ajc" @tap="changeStatus">
			{{status?'账号密码登录':'验证码登录'}}<view class="icon iconfont icon-jinru login-font-color"></view>
		</view>
		<!-- 第三方登录 -->
		<view class="other-login-title u-f-ajc login-padding login-font-color">第三方登录</view>
		<other-login></other-login>
		
		<!-- 协议 -->
		<view class="login-rule u-f-ajc login-padding login-font-color">注册即代表您同意<view>《xxx协议》</view></view>
	</view>
</template>

<script>
	import uniStatusBar from "../../components/uni-status-bar/uni-status-bar.vue"
	import otherLogin from "../../components/home/other-login.vue"
	export default {
		components:{uniStatusBar, otherLogin},
		data() {
			return {
				status:false,//0账号密码登录，1手机验证码登录
				disabled:true,
				loading:false,
				username:'',
				password:'',
				phone:'',
				checknum:'',
				codetime:0
			}
		},
		watch:{
			username(val){
				this.onBtnChange()
			},
			password(val){
				this.onBtnChange()
			},
			phone(val){
				this.onBtnChange()
			},
			checknum(val){
				this.onBtnChange()
			}
		},
		methods: {
			//验证手机号
			isPhone(){
				var mPattern = /^1[34578]\d{9}$/; 
				return mPattern.test(this.phone)
			},
			//获取验证码
			getCheckNum(){
				if(this.codetime > 0){ return;}
				//验证手机号
				var mPattern = /^1[34578]\d{9}$/; 
				if(!this.isPhone()){
					uni.showToast({
						title: '请输入正确的手机号',
						icon:'none'
					});
					return
				}
				//请求服务器，发送验证码
				//发送成功，开启倒计时
				this.codetime = 10
				let timer = setInterval(()=>{
					this.codetime -- ;
					if(this.codetime < 1){
						clearInterval(timer);
						this.codetime = 0
					}
				},1000)
			},
			//初始化表单
			initInput(){
				this.username = ''
				this.password = ''
				this.phone = ''
				this.checknum = ''
			},
			//改变按钮状态
			onBtnChange(){
				if((this.username && this.password) || (this.phone && this.checknum)){
					this.disabled = false
					return
				}
				this.disabled = true
			},
			//切换登录状态
			changeStatus(){
				this.initInput()
				this.status = !this.status
			},
			//返回上一页
			back(){
				uni.navigateBack({
					delta:1
				})
			},
			//提交登录
			submit(){
				//账号密码登录
				if(!this.status){
					return
				}
				// 验证码登录
				if(!this.isPhone()){
					uni.showToast({
						title: '请输入正确的手机号',
						icon:'none'
					});
					return
				}
			}
		}
	}
</script>

<style>
@import "../../common/form.css";
.login-font-color{
	color:#bbb
}
.login-padding{
	padding: 20upx 0;
}
.icon-guanbi{
	position: fixed;
	top: 60upx;
	left: 30upx;
	font-size: 40upx;
	font-weight: bold;
	color: #332f0a;
}
.loginhead{
	width: 100%;
}
.other-login-title{
	position: relative;
}
.other-login-title:before,.other-login-title:after{
	content: '';
	position: absolute;
	background: #bbb;
	height: 1upx;
	width: 100upx;
	top: 50%;
}
.other-login-title:before{
	left: 25%;
}
.other-login-title:after{
	right: 25%;
}
.login-input-box{
	position: relative;
}
.login-input-box .forget-input{
	padding-right: 150upx;
}
.login-input-box .forget,.login-input-box .phone{
	position: absolute;
	top: 0;
	height: 100%;
	z-index: 100;
}
.login-input-box .forget{
	right: 0;
	width: 150upx;
}
.login-input-box .phone{
	left: 0;
	width: 100upx;
	font-weight: bold;
}
.login-input-box .phone-input{
	padding-left: 100upx;
}
.yanzhenma view{
	background: #EEEEEE;
	border-radius: 10upx;
	font-size: 25upx;
	width: 150upx;
	padding: 10upx 0;
}
</style>
