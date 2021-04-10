<template>
	<view class="other-login u-f-ac">
		
		<block v-for="(item,index) in providerList" :key="index">
			<view class="u-f-ajc u-f1" @tap="tologin(item)">
				<view class="icon iconfont u-f-ajc" 
				:class="['icon-'+item.icon]"></view>
			</view>
		</block>
		
	</view>
</template>
<script>
    export default {
        data() {
            return {
                providerList: []
            }
        },
        onLoad() {
            this.getloginAuth()
        },
        methods: {
            //获取登录渠道
            getLoginAuth(){
            	uni.getProvider({
            		service: 'oauth',
            		success: (result) => {
            			this.providerList = result.provider.map((value) => {
            				let providerName = '';
            				let icon='';
            				switch (value) {
            					case 'weixin':
            						providerName = '微信登录';
            						icon='weixin';
            						break;
            					case 'qq':
            						providerName = 'QQ登录';
            						icon='QQ';
            						break;
            					case 'sinaweibo':
            						providerName = '新浪微博登录';
            						icon='xinlangweibo';
            						break;
            					case 'alipay':
            						providerName = '支付宝登录';
            						icon='';
            						break;
            				}
            				return {
            					name: providerName,
            					icon:icon,
            					id: value
            				}
            			});
            			
            		},
            		fail: (error) => {
            			console.log('获取登录通道失败', error);
            		}
            	});
            },
            tologin(provider) {
                uni.login({
                    provider: provider.id,
                    // #ifdef MP-ALIPAY
                    scopes: 'auth_user', //支付宝小程序需设置授权类型
                    // #endif
                    success: (res) => {
                        console.log('login success:', res);
                        // 更新保存在 store 中的登录状态
                        this.login(provider.id);
                    },
                    fail: (err) => {
                        console.log('login fail:', err);
                    }
                });
            }


        }
    }
</script>

<style scoped lang="scss">
    .other-login {
        padding: 20upx 80upx;

        view {
            view {
                width: 100upx;
                height: 100upx;
                border-radius: 100%;
                font-size: 55upx;
                color: #FFFFFF;
            }

            .icon-QQ {
                background: #2CAEFC;
            }

            .icon-xinlangweibo {
                background: #FC7729;
            }

            .icon-weixin {
                background: #2BD19B;
            }
        }
    }
</style>
