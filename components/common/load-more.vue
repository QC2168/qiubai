<template>
    <view class="load-more">
        {{loadtext}}
    </view>
</template>

<script>
    export default {
        props:{
            loadtext:String
        }
    }
    
</script>

<style scoped lang="scss">
    .load-more {
        text-align: center;
        color: #AAAAAA;
        padding: 10upx;
    }
</style>
