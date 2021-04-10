<template>

  <view class="paper-list u-f-ac animated fadeInLeft fast"  @tap="openDetail">
      <image :src="item.userpic" mode="widthFix"></image>
      <view>
          <view class="u-f-ac u-f-jsb">{{item.username}}<text>{{item.time}}</text></view>
          <view class="u-f-ac u-f-jsb">{{item.data}}
          <template v-if="item.noreadnum>=1">
      <uni-badge :text="item.noreadnum" type="error">  </uni-badge>
          </template>
         </view>
      </view>
       </view>

    
</template>

<script>
    import uniBadge from "../../components/uni-badge/uni-badge.vue"
    export default{
        components:{
            uniBadge,
        },
        methods:{
          openDetail(){
              uni.navigateTo({
                  url:'../../pages/user-chat/user-chat'
              })
          }  
        },
        props:{
            item:Object,
            index:Number
        }
    }
</script>

<style lang="scss" scoped>

    .paper-list{
        border-bottom: 1upx solid #EEEEEE ;
        padding: 20upx 0;
        image{
            width: 100upx;
            height: 100upx;
            border-radius: 100%;
            margin-right: 20upx;
            flex-shrink: 0;
        }
        view{
            flex: 1;
            view:first-child{
                font-size: 35upx;
                view{
                    color:#CBCBCB ;
                }
            }
            view:last-child{
                view{
                    color:#999999 ;
                }
            }
        }
        
    }

</style>
