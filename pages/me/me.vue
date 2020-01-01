 <template>
	<view>
		
		<!--主体-->
		<view class="meMain">
			<image src="../../static/icon/meBg.png"></image>
			<view class="mePosition">
				<view class="meMainBox">
					
					<!--头部-->
					<view class="meHead">
						<view class="meHeadAvatar"><image :src="avatarUrl" mode="aspectFill"></image></view>
						<view class="meHeadName"><text @tap="openinfo">{{ nickName }}</text></view>
					</view>
					<!--头部-->
					
					<!--模板-->
					<view class="meOverBg">
						<view class="meVisitor">
							<view class="meVisitorLt">
								<view class="meVisitorTxt_02">0</view>
								<view class="meVisitorTxt_01">模板1</view>
							</view>
							<view class="meVisitorLt">
								<view class="meVisitorTxt_02">0</view>
								<view class="meVisitorTxt_01">模板2</view>
							</view>
						</view>
					</view>
					<!--模板-->
					
					<!--订单-->
					<view class="meOverBg">
						<view class="meVisitorTitle">我的订单</view>
						<view class="meVisitor">
							<view class="meOrderLt">
								<view class="meOrderTxt_01"><image src="../../static/icon/meIcon_01.png"></image></view>
								<view class="meOrderTxt_02">订单1</view>
							</view>
							<view class="meOrderLt">
								<view class="meOrderTxt_01"><image src="../../static/icon/meIcon_01.png"></image></view>
								<view class="meOrderTxt_02">订单2</view>
							</view>
							<view class="meOrderLt">
								<view class="meOrderTxt_01"><image src="../../static/icon/meIcon_01.png"></image></view>
								<view class="meOrderTxt_02">订单3</view>
							</view>
							<view class="meOrderLt">
								<view class="meOrderTxt_01"><image src="../../static/icon/meIcon_01.png"></image></view>
								<view class="meOrderTxt_02">订单4</view>
							</view>
						</view>
					</view>
					<!--订单-->
					
					<!--其他-->
					<view class="meOverBg">
						<view class="businessList">
							<view class="businessListTxt">其他1</view>
							<view class="businessListYou"><image src="../../static/icon/you.png"></image></view>
						</view>
						<view class="businessList">
							<view class="businessListTxt">其他2</view>
							<view class="businessListYou"><image src="../../static/icon/you.png"></image></view>
						</view>
					</view>
					<!--其他-->
					
					<!--其他-->
					<view class="meOverBg">
						<view class="businessList">
							<view class="businessListTxt"><image src="../../static/icon/meIcon_01.png"></image>其他1</view>
							<view class="businessListYou"><image src="../../static/icon/you.png"></image></view>
						</view>
						<view class="businessList">
							<view class="businessListTxt"><image src="../../static/icon/meIcon_01.png"></image>其他2</view>
							<view class="businessListYou"><image src="../../static/icon/you.png"></image></view>
						</view>
					</view>
					<!--其他-->
					
				</view>
			</view>
		</view>
		<!--主体-->
		
	</view>
</template>

<script>
	export default{
		data(){
			return{
				avatarUrl:'../../static/icon/avatar.png',//头像
				nickName:'点击登录',
				token:'',
				loginState:'',
			}
		},
		onLoad() {
			
		},
		onShow() {
			
			this.token = uni.getStorageSync('token');
			
		},
		methods:{
			openinfo(e) {
			    console.log(e)
			    uni.navigateTo({
			        url: '../login/login',
			        success: res => {},
			        fail: () => {},
			        complete: () => {}
			    });
			},
			//点击登录
			BindGetUserInfo:function(){
			
				if ( this.loginState == 1 ) {
					
				} else{
					let that = this;
					wx.getUserInfo({
						success: function (res) {
							//获取到的微信头像 昵称 性别
							that.nickName = res.userInfo.nickName;
							that.avatarUrl = res.userInfo.avatarUrl;
							that.loginState = 1;
						}
					});
				}
			},			
		}
	}
</script>

<style>
	page{ background: #F5F5F5; }
	.meMain{ width: 100%;position: relative; }
	.meMain>image{ width: 100%;height: 220upx;display: block; }
	.meMainBox{ width: 92%;margin: 0 auto; }
	.mePosition{ position: absolute;top: 0;left: 0;width: 100%; }
	.meHead{ overflow: hidden;position: relative; }
	.meHeadAvatar{ float: left;width: 19%;margin-top: 10upx; }
	.meHeadAvatar image{ width: 110upx;height: 110upx;display: block;border-radius: 50%; }
	.meHeadName{ float: left;width: 81%;line-height: 120upx;color: #FFFFFF;font-size: 28upx;overflow:hidden;text-overflow:ellipsis;white-space:nowrap; }
	
	.meOverBg{ background: #FFFFFF;overflow: hidden;border-radius: 12upx;margin-top: 30upx; }
	.meVisitor{ display: flex;flex-direction: row; }
	.meVisitorLt{ width: 50%;text-align: center;margin: 30upx 0; }
	.meVisitorLt:nth-child(1){ border-left: 1px #F5F5F5 solid;border-right: 1px #F5F5F5 solid; }
	.meVisitorTxt_01{ font-size: 28upx;color: #666666; }
	.meVisitorTxt_01 image{ width: 35upx;height: 35upx;vertical-align: middle;margin: 0 10upx 4upx 0; }
	.meVisitorTxt_02{ font-size: 30upx;color: #3B7ED5; }
	
	.meVisitorTitle{ font-size: 30upx;color: #333333;border-bottom: 1px #F5F5F5 solid;padding: 20upx 30upx; }
	.meOrderLt{ width: 25%;text-align: center;padding: 30upx 0;transition: all 0.4s; }
	.meOrderLt:active{ background: #E2E2E2; }
	.meOrderTxt_01{  }
	.meOrderTxt_01 image{ width: 40upx;height: 40upx;display: block;margin: 0 auto 6upx; }
	.meOrderTxt_02{ font-size: 24upx;color: #666666; }
	
	.businessList{ overflow: hidden;padding: 30upx;border-bottom: 1px #F5F5F5 solid;transition: all 0.4s; }
	.businessList:active{ background: #E2E2E2; }
	.businessList:last-child{ border-bottom: none; }
	.businessListTxt{ float: left;font-size: 28upx;color: #333333; }
	.businessListTxt image{ width: 35upx;height: 35upx;vertical-align: middle;margin: 0 10upx 4upx 0; }
	.businessListYou{ float: right;font-size: 28upx;color: #333333; }
	.businessListYou image{ width: 20upx;height: 20upx;vertical-align: middle;margin: 0 0 4upx 10upx; }
	
	
</style>
