<template>
    <view>
        <view class="paper-left-popup-mask" v-show="show" @tap="hidepopup"></view>
        <view class="paper-left-popup" v-show="show">
            <view class="u-f-ac" hover-class="paper-left-popup-h" @tap="addfriend">
                <view class="icon iconfont icon-sousuo"></view>加糗友
            </view>
            <view class="u-f-ac" hover-class="paper-left-popup-h" @tap="clear">
                <view class="icon iconfont icon-qingchu"></view>清除缓存
            </view>
        </view>
    </view>
</template>

<script>
    export default {
        props:{
            show:Boolean
        },
        methods:{
            hidepopup(){this.$emit("hidepopup")},
            addfriend(){this.$emit("addfriend")},
            clear(){this.$emit("clear")}
        }
    }
</script>

<style lang="scss" scoped>
    .paper-left-popup-mask{
          position: absolute;
          right: 0;
          left: 0;
          top:0;
          bottom: 0;
          z-index: 990;
      }
    .paper-left-popup{
        position: fixed;
        right: 0;
        top: 10upx;
        background: #FFFFFF;
        z-index: 1000;
        width: 55%;
        box-shadow: 1upx 1upx 20upx 2upx #CCCCCC;
        .paper-left-popup-h{
            background-color: #EEEEEE;
        }
        view{
            padding: 20upx;
            font-size: 25upx;
            view{
                margin-right: 10upx;
                font-weight: bold;
            }
        }
    }
</style>
