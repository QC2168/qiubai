<template>
    <view class="topic-nav">
        <view class="u-f-ac u-f-jsb">
            <view>热门分类</view>
            <view @tap="toTopicNav">
                更多<text class="icon iconfont icon-jinru"></text>
            </view>
        </view>
        <view class="u-f-ac btm">
            <block v-for="(item,index) in nav" :key="index">
                <view>{{item.name}}</view>
            </block>
        </view>
    </view>
</template>

<script>
    export default {
        props:{
            nav:Object|Array
        },
        methods:{
            toTopicNav(){
                uni.navigateTo({
                    url:"../../pages/topic-nav/topic-nav"
                })
            }
        }
    }
</script>

<style lang="scss" scoped>
    .topic-nav{
        border-bottom: 1upx solid #EEEEEE;
        border-top: 1upx solid #EEEEEE;
        padding: 20upx;
        .btm{
            view{
            display: flex;
            justify-content: center;
            align-items: center;
            flex:1;
            background-color: #DDDDDD;
            color: #9E9E9E;
            border-radius: 10upx;
            margin: 5upx 10upx;
        }
        }
    }
</style>
