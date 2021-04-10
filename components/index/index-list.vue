<template>
 <view>
    
            <view class="index-list animated fadeInUp" @tap="openDetail">
                <view class="index-list1">
                    <view class="left">
                        <image class="headimg" :src="item.userpic" mode="widthFix" lazy-load></image>{{item.username}}
                    </view>
                    <view class="right" v-show="!item.isFollow" @tap="follow">
                        <view class="icon iconfont icon-zengjia follow"></view>关注
                    </view>

                </view>
                <view class="index-list2">{{item.title}}</view>
                <view class="index-list3">
                    <image :src="item.titlePic" mode="widthFix" lazy-load></image>         
              <template v-if="item.type==='video'">
                 <view class="index-list-play icon iconfont icon-bofang"></view>
                 <view class="index-list-playinfo">
                     {{item.playCount}} 播放 {{item.long}}
                 </view>
               </template>
               
               
               
               
                </view>
                <view class="index-list4">
                    <view class="left">
                        <view @tap="operate('ding')">
                            <view v-bind:class="{'active':(item.infoCount.index===1)}" class="icon iconfont icon-icon_xiaolian-mian">{{item.infoCount.dingCount}}</view>
                        </view>
                        <view @tap="operate('cai')">
                            <view v-bind:class="{'active':(item.infoCount.index===2)}" class="icon iconfont icon-kulian">{{item.infoCount.caiCount}}</view>
                        </view>
                    </view>
                    <view class="right">

                        <view>
                            <view class="icon iconfont icon-pinglun">{{item.commentCount}}</view>
                        </view>
                        <view>
                            <view class="icon iconfont icon-zhuanfa">{{item.shareCount}}</view>
                        </view>

                    </view>
                </view>
            </view>

    </view>
</template>

<script>
	export default {
		props:{
            item:Object
        },
        methods:{
            follow(){
                this.item.isFollow=true;
                uni.showToast({
                    title:"关注成功！"
                })
            },
            operate(type){
                // 获取状态
                // 0 没有操作
                // 1 顶
                // 2 踩
                let status =this.item.infoCount.index;
                if(status===0){
                    if(type==='ding'){
                        this.item.infoCount.dingCount++;
                         this.item.infoCount.index=1;
                    }
                    if(type==='cai'){
                          this.item.infoCount.caiCount++;
                           this.item.infoCount.index=2;
                    }
                }
            },
            openDetail(){
                uni.navigateTo({
                    url:"../../pages/detail/detail?detailData="+JSON.stringify(this.item)
                })
            }
        }
	}
</script>

<style scoped lang="scss">
 .index-list {

        padding: 20upx;
        border-bottom: 1upx solid #EEEEEE;

        .index-list1 {
            display: flex;
            justify-content: space-between;
            align-items: center;

            .left {
                display: flex;
                align-items: center;
                color: #999999;
                ;

                .headimg {
                    width: 96upx;
                    height: 96upx;
                    border-radius: 100%;
                    margin-right: 20upx;
                }
            }

            .right {
                display: flex;
                align-items: center;
                justify-content: center;
                background-color: #cacaca;
                border-radius: 10upx;
                padding: 8upx 5upx;
                width: 120upx;
                height: 46upx;

            }

        }

        .index-list2 {
            padding-top: 15upx;
        }

        .index-list3 {
            padding-top: 15upx;
            position: relative;

            image {
                width: 100%;
                border-radius: 20upx;
            }

            .index-list-play {
                position: absolute;
                display: flex;
                justify-content: center;
                align-items: center;
                font-size: 160upx;
                color: white;
                width: 100%;
                height: 100%;
                top: 0upx;
                left: 0;
            }

            .index-list-playinfo {
                position: absolute;
                display: flex;
                justify-content: center;
                align-items: center;
                width: 220upx;
                border-radius: 10upx;
                background-color: #333333;
                color: rgba(255, 255, 255, .6);
                bottom: 26upx;
                right: 11upx;
                padding: 3upx 13upx;

            }

        }

        .index-list4 {
            display: flex;
            justify-content: space-between;
            align-items: center;

            .left,
            .right {
                color: #d8d8d8;

                view {
                    margin: 1upx 5upx;
                }
            }

            .left {
                display: flex;
                align-items: center;


            }

            .right {
                display: flex;
                align-items: center;

            }

        }
    }
</style>
