<template>
	<view class="about">
        <view class="abuot-t u-f-ajc u-f-column">
            <image src="../../static/common/logo.png" mode="widthFix"></image>
            <view>Verrsion 1.0.0</view>
        </view>
		<view class="home-list">
		    <block v-for="(item,index) in list" :key="index">
		        <home-list-item :item="item" :index="index"></home-list-item>
		    </block>
		</view>

        
	</view>
</template>

<script>
    import homeListItem from "../../components/home/home-list-item.vue"
	export default {
        components:{
            homeListItem
        },
		data() {
			return {
				list: [{
				        name: "新版本检测",
				        clicktype: "navigateTo",
				        url: ""
				    },
				    {
				        name: "用户协议",
				        clicktype: "navigateTo",
				        url: ""
				    }
				]
			};
		}
	}
</script>

<style scoped lang="scss">
.about{
    .abuot-t{
        padding: 20upx 0;
        image{
            width: 60%;
            margin-top: 30upx;
            margin-bottom: 20upx;
        }
    }
}
</style>
