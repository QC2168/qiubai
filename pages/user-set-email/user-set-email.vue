<template>
	<view class="body">
		<input v-model="email" type="text" placeholder="输入绑定的邮箱" class="uni-input" />
		<input v-model="password" type="password" placeholder="输入密码" class="uni-input" />

          <button :disabled="btndisabled" @tap="submit" class="user-set-btn" type="primary">完成</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				email:"",
				password:"",
			}
		},
        computed:{
            btndisabled(){
               return !this.email&&this.password;
            }
        },
		methods: {
		    //验证层
		    check(){
		       if(!(this.email&&this.password)){
		           uni.showToast({
		               title:"请将数据填写完整",
		               icon:"none"
		           })
		           return false;
		       }else{
		  
		              return true;
		         
		       }
		    },
		   
		    // 提交
			submit(){
		        if(!this.check())return;
		        uni.showToast({
		            title:"验证通过",
                    mask:false,
                    duration:2000
		        })
                
		     }   
		}
	}
</script>

<style scoped lang="scss">

      @import "../../common/form.css";
</style>

