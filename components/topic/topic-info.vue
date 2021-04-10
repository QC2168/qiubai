<template>
    <view class="topic-detail">
    	<!-- 模糊背景 -->
        <view class="topic-bg">
        	<image :src="item.titlepic" mode="aspectFill" lazy-load></image>
        </view>
        <!-- 话题信息 -->
        <view class="topic-info">
            <view class="topic-info-t u-f-ac">
                <image :src="item.titlepic" mode="aspectFill" lazy-load></image>
            <view>   {{item.title}}</view>
            </view>
            <view class="topic-info-c  u-f-ac">
            <view>动态 {{item.totalnum}}</view>
            <view>评论 {{item.todaynum}}</view>
            </view>
            <view class="topic-info-r">
              {{item.desc}}
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        props:{
            item:Object
        }
    }
</script>

<style lang="scss" scoped>
    .topic-detail{
        .topic-bg{
            width: 100%;
            height: 300upx;
            position: relative;
            overflow: hidden;
            image{
                width: 100%;
                position: absolute;
                filter: blur(10px);
            }
        }
        .topic-info{
            padding: 0 25upx;
            .topic-info-t{
                position: relative;
                image{
                    width: 150upx;
                    height: 150upx;
                    border-radius: 20upx;
                    position: absolute;
                    top: -75upx;
                  
                }
                view{
                    font-size: 35upx;
                    margin-left: 180upx;
                }
            }
            .topic-info-c{
                padding: 35upx 0 15upx 0; 
                view{
                    color: #CDCDCD;
                }
            }
            .topic-info-r{
                color: #A3A3A3;
                  font-size: 32upx;
            }
        }
    }
</style>
