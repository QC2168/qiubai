<template>
    <view class="hoem-list-item u-f-ac u-f-jsb" hover-class="hoem-list-hover" @tap="clickevent">
        <view class="u-f-ac">
            <view class="icon iconfont" :class="['icon-'+item.icon]"></view>{{item.name}}
        </view>
        <view class="icon iconfont icon-jinru" ></view>
    </view>
</template>

<script>
    export default{
        props:{
            item:Object,
            index:Number
        },
        methods:{
            clickevent(){
                let item=this.item;
                switch(item.clicktype){
                    case "navigateTo":
                    if(!item.url)break;
                    uni.navigateTo({url:item.url});
                    break;
                     case "switchTab":
                     if(!this.item.url)break;
                     uni.switchTab({url:item.url})
                       break;
                }
            }
        }
    }
</script>

<style scoped lang="scss">  
    
        .hoem-list-item {
            padding: 20upx;
            border-top: 1upx solid  #F4F4F4;
            border-bottom: 1upx solid #F4F4F4;
    
            view:first-child {
                color: #333333;
               view{
                   margin: 0 10upx;
               }
    
            }
    
            view:last-child {
                color: #CCCCCC;
            }
        }
    
</style>
