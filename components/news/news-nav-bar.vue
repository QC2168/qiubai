<template>
    <view class="news-nav-bar">
        <uni-nav-bar :fixed="true" :statusBar="true" @clickRight="toAdd">
            <!-- left slot -->
            <template v-slot:left>
                <view class="nav-left">
                    <view class="icon iconfont icon-qiandao"></view>
                </view>
            </template>
            <!-- center slot -->
            <template>
                <view class="nav-tab-bar u-f-ajc">
                    <block v-if="Object.keys(tabList).length!==0" v-for="(item,index) in tabList" :key="index">
                        <view @tap="changeTabIndex(index)" :class="{'active':index===tabIndex}">{{item.name}}
                            <view v-if="index===tabIndex" class="nav-tab-bar-line"></view>
                        </view>
                    </block>
                </view>
            </template>
            <!-- right slot -->
            <template v-slot:right>
                <view class="nav-right u-f-ajc">
                    <view class="icon iconfont icon-bianji1"></view>
                </view>
            </template>
        </uni-nav-bar>
    </view>
</template>

<script>
    export default{
        props:{
            tabList:Array,
            tabIndex:Number
        },
        methods:{
            changeTabIndex(index){
                this.$emit("changeTabIndex",index)
            },
            toAdd(){
                this.toAdd("toAdd")
            }
            
        },
        
    }
</script>

<style scoped >
    .nav-left {
        margin-left: 16upx;
    
    }
    
    .nav-left>view {
        color: #FF9619;
        font-size: 32upx;
    }
    
    .nav-right>view {
        font-size: 32upx;
    }
    
    .nav-tab-bar {
        width: 100%;
    }
    
    .nav-tab-bar>view {
        padding: 0 15upx;
        font-size: 35upx;
        font-weight: bold;
        position: relative;
    }
    
    .active {
        color: #333333 !important;
    }
    
    .nav-tab-bar-line {
        width: 100%;
        border-radius: 20upx;
        width: 70upx;
        border-bottom: 10upx solid #FF9619;
        bottom: 0;
    }
    
</style>
