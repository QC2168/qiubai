<template>
	<view class="body">
		<input v-model="oldpassword" type="password" placeholder="输入旧密码" class="uni-input" />
		<input v-model="newpassword" type="password" placeholder="输入新密码" class="uni-input" />
		<input v-model="renewpassword" type="password" placeholder="确认新密码" class="uni-input" />
          <button :disabled="btndisabled" @tap="submit" class="user-set-btn" type="primary">完成</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				oldpassword:"",
				newpassword:"",
				renewpassword:"",
			}
		},
        computed:{
            btndisabled(){
               return !this.oldpassword&&this.newpassword&&this.renewpassword;
            }
        },
		methods: {
            //验证层
            check(){
               if(!(this.oldpassword&&this.newpassword&&this.renewpassword)){
                   uni.showToast({
                       title:"请将数据填写完整",
                       icon:"none"
                   })
                   return false;
               }else{
                  if(this.newpassword===this.renewpassword){
                      uni.showToast({
                          title:"密码不一致",
                          icon:"none"
                      })
                       return false;
                  }else{
                      return true;
                  }
               }
            },
           
            // 提交
			submit(){
                if(!this.check())return;
                uni.showToast({
                    title:"验证通过",
                    icon:"none"
                })
             }   
		}
	}
</script>

<style scoped lang="scss">

      @import "../../common/form.css";
</style>
