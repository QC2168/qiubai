<template>
    <view class="uni-tab-bar">
        <scroll-view scroll-x class="uni-swiper-tab" :style="scrollStyle">
            <block v-for="(tab,index) in tabBars" :key="index">
                <view class="swiper-tab-list" style="width: 50%;" :style="scrollItemStyle" :class="{'active':index===tabIndex}" @tap="tabtap(index)">
                    {{tab.name}}{{tab.num?tab.num:''}}
                    <view class="swiper-tab-line"></view>
                </view>
            </block>
        </scroll-view>
        </view>
</template>

<script>
    export default {
        props:{
            tabBars:Array,
            tabIndex:Number,
            scrollStyle:{
                type:String,
                default:""
            },
            scrollItemStyle:{
                type:String,
                default:""
            }
            
        },
        methods:{
            // 获取事件
            tabChange(e) {
                this.tabIndex = e.detail.current;
            },
            //点击事件
            tabtap(index) {
                this.$emit('tabtap',index)
            }
        }
    }
    
</script>

<style scoped lang="scss">
    .uni-swiper-tab {
        border-bottom: 1upx solid #EEEEEE;
    
        .swiper-tab-list {
            color: #969696;
            font-weight: blue;
    
        }
        .active {
            color: #343434;
        
            .swiper-tab-line {
                border-bottom: 6upx solid #FEDE33;
                width: 70px;
                margin: auto;
                border-top: 6upx solid #FEDE33;
                border-radius: 10upx;
            }
        }
    }
</style>
