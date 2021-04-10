<template>
    <view class="topic-new">
        <view>最近更新</view>
       <view class="topic-list u-f animated fadeInLeft fast" @tap="opendetail">
            <image :src="item.titlepic" lazy-load mode="widthFix"></image>
        <view>
            <view>{{item.title}}</view>
            <view>{{item.desc}}</view>
            <view>动态 {{item.totalnum}} 今日 {{item.todaynum}}</view>
            </view>
        </view>
    </view>
</template>

<script>
    export default{
        props:{
           item:Object,
           index:Number
        },
        methods:{
            opendetail(){
                uni.navigateTo({
                    url:"../../pages/topic-detail/topic-detail"
                })
            }
        }
    }
</script>

<style scoped lang="scss">
    .topic-new{
        padding: 20upx;
        border-bottom: 1upx solid #EEEEEE;
        view:first-child{
    
            font-size: 32upx;
            image{
                
            }
        }
        .topic-list{
            padding: 10upx 0;
            image{
                width: 150upx;
                height: 150upx;
                border-radius: 10upx;
                margin-right: 10upx;
            }
            view{
                view:first-child{
                    font-weight: bold;
                    font-size: 28upx;
                }
            }
        }
    }
</style>
