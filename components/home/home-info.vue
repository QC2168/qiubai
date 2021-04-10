<template>
    <view class="home-info u-f-ac">
        <image :src="homeinfo.userpic" mode="scaleToFill" lazy-load></image>
        <view class="u-f1">
            <view>{{homeinfo.username}}</view>
            <view>总访客 {{homeinfo.totalnum}} 今日 {{homeinfo.todaynum}}</view>
        </view>
        <view class="icon iconfont icon-jinru"></view>
    </view>
</template>

<script>
    export default{
        props:{
            homeinfo:Object,
        }
    }
</script>

<style scoped lang="scss">
    .home-info {
        padding: 20upx 40upx;
    
        image {
            flex-shrink: 0;
            width: 90upx;
            height: 90upx;
            border-radius: 100%;
            margin-right: 15upx;
        }
    
        view:first-of-type {
            view:first-child {
                font-size: 32upx;
            }
        }
    
        view:last-of-type {
            view:first-child {
                // font-size:32upx;
                color: #BBBBBB;
            }
        }
    
        view:last-of-type {
            height: 100%;
    
        }
    }
</style>
