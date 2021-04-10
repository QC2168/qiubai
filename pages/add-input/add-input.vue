<template>
    <view>
        <!-- 自定义导航 -->
        <view class="example-body">
            <uni-nav-bar :statusBar="true" left-icon="arrowleft" rightText="发布" @clickLeft="back" @clickRight="submit">
                <view class="u-f-ajc" @tap="changelook">
                    {{privacy}}
                    <view class="icon iconfont icon-xialazhankai"></view>
                </view>
            </uni-nav-bar>
        </view>

        <!-- 多行输入框 -->
        <view class="uni-textarea">
            <textarea v-model="text" placeholder="说一句话吧？" />
            </view>
        <!-- 上传多图 -->
        <view>
        <upload-images
           @upload="upload"
        ></upload-images>
        </view>
        <!-- 弹出公告 -->
<uni-popup ref="popup" type="center" @change="change">
<view class="popup u-f-ajc">
    <image class="img " src="../../static/common/addinput.png" mode="widthFix"></image>
    <ul>
        <li>1、涉及黄色，政治,广告及骚扰信息</li>
        <li>2、涉及人身攻击</li>
        <li>3、留联系方式，透露他人隐私</li>
        <li>一经核实将被封禁,情节严重者永久封禁</li>
    </ul>
</view>
		</uni-popup>
       
    </view>
</template>

<script>
    let changeLook = ['所有人可见', '仅自己可见'];
    import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue"
    import uploadImages from "../../components/common/uploud-images.vue"
    import uniPopup from "../../components/uni-popup/uni-popup.vue"
    export default {
        components: {
            uniNavBar,uploadImages,uniPopup
        },
        created() {
          
        },
        mounted() {
           this.togglePopup('togglePopup','popup')
        },
        data() {
            return {
                isGet:false,
                showpopup:true,
                privacy: "所有人可见",
                text:"",
                imageList: [],
               
            };
        },
        methods: {
            // 保存为初稿
            save(){
                uni.showModal({
                    content:"是否要保存草稿?",
                    cancelText:"不保存",
                    confirmText:"保存",
                    success: (res) => {
                        if(res.confirm){
                            console.log(1)
                        }else{
                            console.log(2)
                        }
                        this.isGet=true;
                        uni.navigateBack({
                            delta:1
                        })
                    }
                });
            },
            
            change(e){
                console.log(e)
            }, 
            // 返回
            back() {
                uni.navigateBack({
                    delta: 1
                });
            },
            // 发布
            submit() {

            },
            // 隐私
            changelook() {
                uni.showActionSheet({
                    itemList:changeLook,
                    success: (res) => {
                            this.privacy = changeLook[res.tapIndex];
                    }
                });
            },
            upload(arr){
                this.imageList=arr;
            },
            togglePopup(type, open) {
            	this.$nextTick(() => {
            		this.$refs['popup'].open()
            	})
            },
            // 判断用户使用返回
            onBackPress(){
                // 如果有值
                if(!this.text || this.imageList.length!==0){
                    console.log(123)
                    return
                }
                if(!this.isGet){
                    this.save();
                  return true;
                }

                
            }
       
        }
    }
</script>

<style lang="scss" scoped>
.uni-textarea{
    border: 1upx soild #EEEEEE;
}
.cell-pd {
		padding: 22rpx 30rpx;
	}

	.list-pd {
		margin-top: 50rpx;
	}
    .uni-uploader__file{
        position: relative;
 .icon-shanchu{
        position: absolute;
        right: 0;
        top: 0;
        background-color: #333333;
        color:#FFFFFF;
        padding: 2upx 10upx;
        border-radius: 10upx;
    }
    }
    .popup{
        width: 600upx;
        height: 400upx;
        background-color: rgb(255,255,255);
        border-radius: 10upx;
        flex-direction: column;
        .img{
            margin: 20upx;
            width: 270upx;         
        }
        ul{
                list-style-type: none;
        }
    }
  
</style>
