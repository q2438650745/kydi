<template>
	<!--首页-->
	<view>
		
		<!--头部导航-->		
		<view class="headNav">
			<view class="headNavBox">
				<scroll-view scroll-x="true" scroll-top>
					<view class="headNavLt" v-for="(item,index) in headTabList" :key="index" :class="{activeNav:index == headTabIdx}" @click="IsHeadTabClick(index,item)">
						{{ item.name }}
					</view>
				</scroll-view>
			</view>
		</view>
		<!--头部导航-->
		
		<!--主体-->
		<view class="idxMain">
			
			<!--轮播图-->
			<swiper class="swiper" indicator-active-color='#fff' :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
				<swiper-item v-for="(item,index) in bannerList" :key='index' @click="JumpFuneralNews(index,item)">
					<view class="swiper-item uni-bg-red">
						<image :src="item.imgs"></image>
					</view>
					<view class="swiper-title">
						<view class="swiper-title-box">{{ item.title }}</view>
					</view>
				</swiper-item>
			</swiper>
			<!--轮播图-->
			
			<!--内容1-->
			<view class="contBg">
				<view class="contOver" v-for="(item,index) in contOneList" :key="index">
					<view class="idxMainBox">
						<view class="contOverLt">
							<view class="contTxt">{{ item.title }}</view>
							<view class="contTime">{{ item.author }} {{ item.updateTime }}</view>
						</view>
						<view class="contRtImg"><image :src="item.imgs"></image></view>
					</view>
				</view>
			</view>
			<!--内容1-->
			
			<!--内容2-->
			<view class="shopOver">
				<view class="contTitle">
					<view class="idxMainBox">推荐商品</view>
				</view>
				<view class="idxMainBox">
					<view class="shopLt" v-for="(item,index) in contTwoList" :key='index'>
						<view class="shopImg"><image :src="item.imgs" mode="aspectFill"></image></view>
						<view class="shopTxt">{{ item.name }}</view>
						<view class="shopMoney"><text>￥{{ item.money }}</text><text>/剩余{{ item.yu }}</text></view>
					</view>
				</view>
			</view>
			<!--内容2-->
			
			<!--内容3-->
			<view class="contBg">
				<view class="contTitle">
					<view class="idxMainBox">最新资讯</view>
				</view>
				<view class="newsOver">
					<view class="idxMainBox">
						<view class="newsTitle">资讯标题资讯标题资讯标题资讯标题资讯标题资讯标题</view>
						<view class="newsImg"><image src="../../static/banner.jpg" mode="aspectFit"></image></view>
						<view class="newsTime"><text>浏览：50</text><text>2019-07-30</text></view>
					</view>
				</view>
			</view>
			<!--内容3-->
			
		</view>
		<!--主体-->
		
		
		
		<!--抽空会更新模板-->
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				headTabList:[
					{ id:0, name:'导航导航1' },
					{ id:1, name:'导航1' },
					{ id:2, name:'导航1' },
					{ id:3, name:'导航导航1' },
					{ id:4, name:'导航导航1' },
					{ id:5, name:'导航导航1' },
				],//头部导航
				headTabIdx:0,
				
				bannerList:[
					{ id:1, imgs:'../../static/banner.jpg' },
					{ id:2, imgs:'../../static/banner.jpg' }
				],//轮播图
				
				contOneList:[
					{ id:1, title:'啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊', author:'平台', updateTime:'2019-7-30', imgs:'../../static/banner.jpg' },
					{ id:2, title:'啊啊啊啊啊啊', author:'平台', updateTime:'2019-7-30', imgs:'../../static/banner.jpg' },
				],//内容1
				
				contTwoList:[
					{ id:1, imgs:'../../static/banner.jpg', name:'商品商品商品商品', money:'50', yu:'50' },
					{ id:2, imgs:'../../static/banner.jpg', name:'商品商品商品商品', money:'50', yu:'50' },
				],//内容2
				
				/*图片轮播*/
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500,
				
			}
		},
		onLoad() {
			
		},
		methods: {
			
			//首页头部tab点击切换
			IsHeadTabClick: function(index,item){
				this.headTabIdx = index;
			},
			
			
			//官网复制的轮播
			changeIndicatorDots(e) {
				this.indicatorDots = !this.indicatorDots
			},
			changeAutoplay(e) {
				this.autoplay = !this.autoplay
			},
			intervalChange(e) {
				this.interval = e.target.value
			},
			durationChange(e) {
				this.duration = e.target.value
			}
			
		}
	}
</script>

<style>
	page{ background: #F5F5F5; }
	.headNav{ 
		width: 100%;
		background: #FFFFFF;
		white-space: nowrap; 
		position: fixed;
		top: 0;
		left: 0;
		z-index: 15;
		border-bottom: 1px #F2F2F2 solid;
	}
	.headNavBox{ width: 92%;margin: 0 auto; }
	.headNavLt{	display: inline-block;height: 100upx;line-height: 100upx;font-size: 30upx;margin-right: 30upx; }
	.headNavLt:last-child{ margin-right: 0; }
	.activeNav{ color: #3B7ED5; }
	.swiper{  height: 307rpx; }
	.swiper-item image{ width: 100%;height: 307rpx;display: block; }
	
	.idxMain{ width: 100%;padding-top: 100upx; }
	.idxMainBox{ width: 92%;margin: 0 auto; }
	.contBg{ background: #FFFFFF;overflow: hidden;margin-bottom: 30upx; }
	
	.contOver{ border-bottom: 1px #EDEDED solid;overflow: hidden;transition: all 0.4s; }
	.contOver:active{ background: #E2E2E2; }
	.contOver:last-child{ border-bottom: none; }
	.contOverLt{ float: left;width: 60%; }
	.contTxt{
		color: #333333;
		font-size: 30upx;
		width: 100%;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp:2;
		-webkit-box-orient:vertical;
		overflow: hidden;
		padding-top: 30upx;
	}
	.contTime{ color: #888888;font-size: 24upx;margin-top: 30upx; }
	.contRtImg{ float: right;width: 35%;height: 155upx;margin: 30upx 0; }
	.contRtImg image{ width: 100%;height: 100%;display: block;border-radius: 6upx; }
	
	.contTitle{ background: #FFFFFF;font-size: 30upx;color: #3B7ED5;height: 80upx;line-height: 80upx;border-bottom: 1px #F5F5F5 solid; }
	.shopOver{ overflow: hidden;margin-bottom: 30upx; }
	.shopLt{ 
		float: left;
		width: 48.5%;
		background: #FFFFFF;
		height: 360upx;
		border: 1px #F2F2F2 solid;
		border-radius: 12upx;
		transition: all 0.4s;
		margin-top: 15upx;
	}
	.shopLt:nth-child(2n){ float: right; }
	.shopLt:active{ background: #E2E2E2; }
	.shopImg{ height: 220upx; }
	.shopImg image{ width: 100%;height: 100%;display: block;border-radius: 12upx 12upx 0 0; }
	.shopTxt{ font-size: 28upx;color: #333333;padding: 20upx 20upx 0 20upx;display:block;white-space:nowrap; overflow:hidden; text-overflow:ellipsis; }
	.shopMoney{ padding: 0 20upx; }
	.shopMoney text{ font-size: 26upx;color: red; }
	.shopMoney text:last-child{ color: #aaaaaa; }
	
	.newsOver{ border-bottom: 1px #F5F5F5 solid;transition: all 0.4s; }
	.newsOver:active{ background: #E2E2E2; }
	.newsOver:last-child{ border-bottom: none; }
	.newsTitle{ 
		font-size: 30upx;
		color: #333333;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp:3;
		-webkit-box-orient:vertical;
		overflow: hidden;
		padding: 30upx 0 20upx 0;
		text-align: justify;
	}
	.newsImg{ height: 360upx;border: 1px #F5F5F5 solid; }
	.newsImg image{ width: 100%;height: 100%;display: block; }
	.newsTime{ overflow: hidden;padding: 20upx 0 30upx 0; }
	.newsTime text{ font-size: 26upx;color: #AAAAAA;float: left; }
	.newsTime text:last-child{ float: right; }
	
</style>
