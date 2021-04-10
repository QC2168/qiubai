<template>
    <view>
        <uni-collapse>
        	<uni-collapse-item v-for="(item,index) in list" :key="index" :title="item.title" show-animation>
        		<text class="content" style="padding: 30upx;">{{item.content}}</text>
        	</uni-collapse-item>
        </uni-collapse>
        <view class="body">
        	 <button @tap="submit" class="user-set-btn" type="primary">反馈</button>
        </view>
    </view>

</template>

<script>
    import uniCollapseItem from "../../components/uni-collapse-item/uni-collapse-item.vue"
    import uniCollapse from "../../components/uni-collapse/uni-collapse.vue"
	export default {
        components:{
          uniCollapseItem,
          uniCollapse
        },
		data() {
			return {
				list:[
                    {
                        title:"客服什么时候上线",
                        content:"9点-18点"
                    },
                    {
                        title:"忘记账户密码怎么办",
                        content:"找回密码"
                    },
                    {
                        title:"忘记账户密码怎么办",
                        content:"找回密码"
                    },
                ]
			};
		}
	}
</script>

<style lang="scss">
@import "../../common/form.css";
</style>
