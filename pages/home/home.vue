<template>
    <view class="home">
        <!-- 登录 -->
      <template v-if="islogin">
          <home-info :homeinfo="homeinfo"></home-info>
      </template>
        <template v-else>
            <!-- 未登录 -->
            <view class="u-f-ajc">登录，体验更多功能</view>
            <!-- 第三方登录 -->
            <other-login />
            <!--账号密码登录 -->
            <view class="u-f-ajc" @tap="openLogin">账号密码登录<view class="icon iconfont icon-jinru"></view>
            </view>
        </template>
       

        <!-- 数据 -->
        <view class="home-data  u-f-ac">
         <home-data :homedata="homedata"></home-data>
          
        </view>

        <!-- 广告位 -->
        <view class="home-adv u-f-ajc">
            <image mode="widthFix" src="../../static/demo/demo20.jpg"></image>
        </view>

        <!-- 功能列表 -->
        <view class="home-list">
            <block v-for="(item,index) in list" :key="index"> 
                <home-list-item :item="item" :index="index"></home-list-item>
            </block>
        </view>
    </view>
</template>

<script>
    import uniList from "../../components/uni-list/uni-list.vue"
    import homeListItem from "../../components/home/home-list-item.vue"
    import homeInfo from "../../components/home/home-info.vue"
    import otherLogin from "../../components/home/other-login.vue"
    import homeData from "../../components/home/home-data.vue"
    export default {
        components: {
            uniList,
            homeListItem,
            homeInfo,
            otherLogin,
            homeData
        },
        data() {
            return {
                islogin: false,
                homeinfo:{
                    userpic:"../../static/demo/datapic/10.jpg",
                    username:"黄新泓",
                    totalnum:6888,
                    todaynum:90
                },
                homedata:[
                  {name:"糗事",num:0},  
                  {name:"动态",num:0},  
                  {name:"评论",num:0},  
                  {name:"收藏",num:0}  
                ],
                list:[
                    {
                        icon:"liulan",name:"浏览记录"
                    },
                    {
                        icon:"huiyuanvip",
                        name:"糗百认证",
                        clicktype:"糗百认证",
                        url:"糗百认证",
                    },
                    {
                        icon:"keyboard",
                        name:"审核糗事",
                        clicktype:"审核糗事",
                        url:"审核糗事",
                    },
                ]
                }
        },
        methods: {
openLogin(){
    uni.navigateTo({
        url:"../login/login"
    })
}
        },
        onNavigationBarButtonTap(e) {
            if (e.index === 0) {
               uni.navigateTo({
                   url:"../user-set/user-set"
               })
            }
        }
    }
</script>

<style scoped lang="scss">
    .home {
        .home-adv {
            padding: 20upx;
            height: 150upx;

            image {
                border-radius: 20upx;
            }
        }

        

        .hoem-list-hover {
            background-color: #F4F4F4;
        }
    }
</style>
