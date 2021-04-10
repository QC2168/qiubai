<template>
	<view class="body">
        <!-- 操作菜单 -->
        <paper-left-popup @hidepopup="hidepopup" @addfriend="addfriend" @clear="clear"></paper-left-popup>
        <!-- 小纸条列表 -->
        <block v-if="Object.keys(list).length!==0" v-for="(item,index) in list" :key="index">
            <paper-list :item="item" :index="index"></paper-list>
        </block>
        <!-- 上拉加载 -->
        <load-more :loadtext="loadtext"></load-more>
	</view>
</template>

<script>
    import uniBadge from "../../components/uni-badge/uni-badge.vue"
    import paperList from "../../components/paper/paper-list.vue"
     import loadMore from "../../components/common/load-more.vue"
     import paperLeftPopup from "../../components/paper/paper-left-popup.vue"
	export default {
        components:{
            uniBadge,
            paperList,loadMore,paperLeftPopup
            
        },
		data() {
			return {
                show:false,
                loadtext:"上拉加载更多",
				list:[
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:1
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:12
                    }
                ]
			}
		},
        onReachBottom(){
            this.loadmore()
            
        },
		methods: {
            addfriend(){
              this.show=false
            },
            clear(){
               this.show=false
            },
            hidepopup(){
                this.show=false
            },
            showpopup(){
                 this.show=true
            },
            loadmore(index) {
                if (this.loadtext != "上拉加载更多") {
                    return;
                }
                // 修改状态
                this.loadtext = "上拉加载更多"
                // 获取数据
            
                // 获取成功
                this.loadtext = "加载中..."
                // this.newsList[index].loadtext = "没有数据啦！"
                setTimeout(() => {
                    let obj =  {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥",
                        noreadnum:12
                    }
                    // 添加数据
                    this.list.push(obj)
                    this.loadtext = "上拉加载更多"
                }, 500)
            
            },
            //获取数据
			getdata(){
                let arr=[
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥a1",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥a1",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥a1",
                        noreadnum:0
                    },
                    {
                       userpic:"../../static/demo/userpic/12.jpg",
                        username:"黄新泓",
                        time:"1:12",
                        data:"你好呀 小哥哥a1",
                        noreadnum:12
                    }
                ];
                
                //关闭下拉刷新
                setTimeout(()=>{
                    this.list=arr;
                    uni.stopPullDownRefresh();
                },1000)
            }
		},
        //监听导航点击事件
        onNavigationBarButtonTap(e){
            switch(e.index){
                case 0:
                uni.navigateTo({
                    url:"../user-list/user-list"
                })
                break;
                case 1:
                this.showpopup();
                  break;
            }
        },
        onPullDownRefresh() {
            //监听下拉
            this.getdata()
        }
	}
</script>

<style lang="scss" scoped>
.body{
    
    padding: 0 20upx;
   
}
</style>
