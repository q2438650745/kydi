<template>
	<view class="s-page-wrapper is-100vh">
		<view class="is-33vh has-mgt-10">
			<view class="is-flex is-column is-justify-center  is-align-center is-height-100">
				<image src="../../static/logo.png" mode="aspectFit" class="logoimg"></image>
			</view>
		</view>
		<view class="content">
			<view class="has-mglr-10 ">
				<view class=" has-mgtb-10 ">
					<input type="number" maxlength="11" v-model="login.username" placeholder="请输入用户名" class="is-input1 " @input="BindInput" />
				</view>
				<view class=" has-radius has-mgtb-10">
					<input v-model="login.password" placeholder="请输入登录密码" class="is-input1"  @input="BindInput" type="password"/>
				</view>

				<view class=" loginbtn has-radius has-mgtb-20">
					<button :loading="login.loading" @tap="defaultHandlerLogin"> {{ login.loading ? "登录中...":"登 录"}} </button>
				</view>
			</view>
		</view>
		<view class="is-20vh has-mgt-80 content">
			<navigator url="#" class=" has-radius is-right is-grey has-mgr-20" hover-class="">
				<text>没有账号？</text><text class="is-blue" @tap="openregister">点击注册</text>
			</navigator>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				login: {
					username:"",
					password:""
				},
				loading: false,
			};
		},
		methods:{
			defaultHandlerLogin:function(){
				this.loading = true;
				uni.request({
				    url: 'http://47.104.180.97:8080/miniApi/login', 
					method: "POST",
				    data: this.login,
				    success: (res) => {
						this.loading = false;
				        console.log(res.data);
				    },
					fail: (res) => {
						this.loading = false;
						console.log(res.data);
					}
				});
			},
			BindInput:function(e){
				var dataval = e.currentTarget.dataset.val;
				this.login[dataval] = e.detail.value; 
			},
			openregister:function(e){
				console.log(e)
				uni.navigateTo({
				    url: '../login/register',
				    success: res => {},
				    fail: () => {},
				    complete: () => {}
				});
			}
		}
	}
</script>

<style>
	page {
		min-height: 100%;
		background-color: #FFFFFF;
	}

	.content {
		width: 85%;
		margin: 0 auto;
	}

	.loginbtn button {
		margin-top: 20rpx;
		height: 88rpx;
		width: 100%;
		line-height: 88rpx;
		color: #ffffff;
		font-size: 32rpx;
		border-radius: 44rpx;
		outline: 0;
		display: block;
		margin: 0;
		font-family: inherit;
		background: #f35;
		opacity: 0.8;
	}

	button:after {
		border: 2rpx solid #f2f2f2;
	}

	.logoimg {
		width: 200rpx;
		height: 200rpx;
		border-radius: 50%;
	}

	.is-input1 {
		height: 88rpx;
		width: 100%;
		line-height: 88rpx;
		padding: 12rpx;
		color: #353535;
		font-size: 32rpx;
		box-sizing: border-box;
		appearance: none;
		border: 2rpx solid #e5e5e5;
		box-shadow: none;
		border-radius: 44rpx;
		outline: 0;
		display: block;
		padding-left: 30rpx;
		margin: 0;
		font-family: inherit;
		background: #fff;
		resize: none;
	}
</style>
