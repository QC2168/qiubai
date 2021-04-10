<template>
    <view class="user-list u-f-ac animated fadeInLeft fast">
        <image :src="item.userpic" mode="widthFix" lazy-load></image>
            <view>
                <view>{{item.username}}</view>
                
                <tag-sex-age :sex="item.sex" :age="item.age"></tag-sex-age>
            </view>
            <view class="iconnzj icon iconfont "
            :class="[item.isguanzhu?'iconn icon-xuanze-yixuan':'iconnzj icon-zengjia1']"
            ></view>
    </view>
</template>

<script>
        import tagSexAge from "../../components/common/tag-sex-age.vue"
    export default {
        components: {
            tagSexAge
        },
      
        props:{
            item:Object,
            index:Number
        }
    }
</script>

<style lang="scss" scoped>
    .user-list{
        padding: 20upx 0;
        border-bottom: 1upx solid #EEEEEE;
        image{
            width: 100upx;
            height: 100upx;
            border-radius: 100%;
            margin:0 30upx;
            flex-shrink: 0;
        }
        view{
            .iconn{
                position: absolute;
                right: 20upx;
                
            }
            .iconnzj{
                color: #F8791B!important;
                position: absolute;
                right: 20upx;
            }
        }
    }
</style>
