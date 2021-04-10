<template>
    <view class="login">
        <!-- 状态栏 -->
        <uni-status-bar bgcolor="#FFE933"></uni-status-bar>
        <!-- 关闭按钮 -->
        <view class="icon iconfont icon-guanbi" @tap="back"></view>
        <view>
            <image class="loginhead" src="../../static/common/loginhead.png" mode="widthFix"></image>
        </view>
        <!-- 输入框  按钮 -->
       <view class="body">
<!-- 账号密码登录 -->
<template v-if="status===0">
  <input v-model="username" type="text" placeholder="请输入账户" class="uni-input" />
              <view class="login-input-box">
                  <input v-model="password" type="password" placeholder="请输入密码" class="uni-input forget-input" />
                  <view class="forget u-f-ajc">忘记密码</view>
              </view>
              <button :disabled="userBtnDisabled" @tap="submit" class="user-set-btn" type="primary">登录</button>
    
</template>
<!-- 手机验证码登录 -->
<template v-else>
    <view class="login-input-box">
          <view class="phone u-f-ajc">+86</view>
          <input v-model="phone" type="text" placeholder="请输入手机号" class="uni-input phone-input" />
      </view>
    <view class="login-input-box">
        <input v-model="checknum" type="password" placeholder="请输入验证码" class="uni-input forget-input" />
        <view class="forget u-f-ajc yzm" @tap="getChecknum">{{!codetime?"获取验证码":codetime+' 秒'}}</view>
    </view>
    <button :disabled="phoneBtnDisabled" @tap="submit" class="user-set-btn" type="primary">登录</button>
    
</template>


        </view>
      
   
        <!-- 登录状态切换 -->
        <view class="login-status u-f-ajc login-padding login-font-color" @tap="changeStatus">
            {{status===0?'验证码登录':'账号密码登录'}}<view class="icon iconfont icon-jinru"></view>
        </view>

        <!-- 第三方登录 -->
        <view class="other-login-title u-f-ajc login-padding login-font-color">第三方登录</view>
        <other-login></other-login>

        <!-- 协议 -->
        <view class="login-rule u-f-ajc login-padding login-font-color">
            注册即代表您同意<view style="color: #007AFF;">《仿糗事百科协议》</view>
        </view>
    </view>
</template>

<script>
    import uniStatusBar from "../../components/uni-status-bar/uni-status-bar.vue"
    import otherLogin from "../../components/home/other-login.vue"
    export default {
        components: {
            uniStatusBar,
            otherLogin
        },
        computed:{
            userBtnDisabled(){
                return !this.username&&this.password
            },
            phoneBtnDisabled(){
                return !this.phone && this.checknum
            }
        },
        data() {
            return {
                status:0,
                // 0 当前账号密码登录   1  验证码登录
                
                username:"",
                password:"",
                phone:"",
                checknum:"",
                codetime:0
            }
        },
        methods: {
            //判断手机号是否正规
            checkPhone(){
                 if(!(/^1[3456789]\d{9}$/.test(this.phone))){ 
                
                        uni.showToast({
                            title:"手机号有误",
                            icon:'none'
                        }) 
                        return false; 
                    } else{
                  
                        return true;
                    }
            },
            //获取验证码
            getChecknum(){
                if(!this.checkPhone())return;
                if (this.codetime>0)return;
                //请求服务器  发验证码，开启倒计时
                this.codetime=10;
                let timer=setInterval(()=>{
                    this.codetime--;
                    if(this.codetime<1)clearInterval(timer)
                },1000)
                
            },
            //切换登录模式
            changeStatus(){
                this.status===0?this.status=1:this.status=0;
            },
            // 返回上一步
            back() {
                uni.navigateBack({
                    delta: 1
                })
            },
            submit() {

            }
        }
    }
</script>

<style lang="scss">
    @import "../../common/form.css";

    .login {
        .body{
            .login-input-box{
                position: relative;
                .phone{
                    position: absolute;
                    left: 20upx;
                    top:0;
                    width: 50upx;
                    height: 100%;
                    font-weight: bold;
                }
                .forget{
                    position: absolute;
                    right: 0;
                    top:0;
                    width: 150upx;
                    height: 100%;
                    
                }
                .yzm{
                    background-color: #EEEEEE;
                    border-radius: 10upx;
                    font-size: 25upx;
                    padding: 0 5upx;
                    
                }
                .phone-input{
                    padding-left: 85upx;
                }
                .forget-input{
                    padding-right: 160upx;
                }
           
            }
        }
        .other-login-title {
            position: relative;
        }

        .other-login-title:before,
        .other-login-title:after {
            content: "";
            position: absolute;
            background-color: #CCCCCC;
            height: 1upx;
            width: 100upx;
            top: 50%
        }

        .other-login-title:before {
            left: 20%;
        }

        .other-login-title:after {
            right: 20%;
        }

        .login-font-color {
            color: gray;
        }

        .login-padding {
            padding: 20upx 0;
        }

        .icon-guanbi {
            position: fixed;
            top: 60upx;
            left: 30upx;
            font-size: 40upx;
            color: black;
            font-weight: bold;
        }

        .loginhead {
            width: 100%;
        }

    }
</style>
