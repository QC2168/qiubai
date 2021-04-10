<template>
	<view :style="{ height: statusBarHeight,backgroundColor: bgcolor }" class="uni-status-bar">
		<slot />
	</view>
</template>

<script>
	var statusBarHeight = uni.getSystemInfoSync().statusBarHeight + 'px'
	export default {
		name: 'UniStatusBar',
        props:{
          bgcolor:{
              type:String,
              default:''
          }
        },
		data() {
			return {
				statusBarHeight: statusBarHeight
			}
		}
	}
</script>

<style scoped>
	.uni-status-bar {
		width: 750rpx;
		height: 20px;
		height: var(--status-bar-height);
        

	}
</style>