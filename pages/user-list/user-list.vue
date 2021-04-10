<template>
    <view class="user-list">
        <swiper-tab-head srcollStyle="border-bottom:0;" scrollItemStyle="width:33.3%" @tabtap="tabtap" :tabBars="tabBars"
            :tabIndex="tabIndex"></swiper-tab-head>
            <!-- 好友列表 -->
       
            <view class="uni-tab-bar">
                <swiper class="swiper-box" :style="{height:swiperheight+'px'}" :current="tabIndex" @change="tabChange">
                    <swiper-item v-for="(items,index) in newsList" :key="index">
                        <scroll-view scroll-y class="list" @scrolltolower="loadmore(index)">
                            <template v-if="items.list.length!==0">
                                <view>
                                    <!-- 图文列表-->
                                 <block v-for="(item,index1) in items.list" :key="index1">
                                     <user-list :item="item" :index="index1"></user-list>
                                 </block>
                                    <!-- 上拉加载-->
                                    <load-more :loadtext="items.loadtext"></load-more>
                                </view>
                            </template>
            
                            <template v-if="items.list.length===0">
                                <!-- 无内容默认-->
                                <no-thing></no-thing>
                            </template>
            
                        </scroll-view>
                    </swiper-item>
                </swiper>
            </view>
           
    </view>
</template>

<script>
    import swiperTabHead from "../../components/index/swiper-tab-head.vue"
    import userList from "../../components/user-list/user-list.vue"
       import loadMore from "../../components/common/load-more.vue"
           import noThing from "../../components/common/no-thing.vue"
    export default {
        components: {
            swiperTabHead,userList,loadMore,noThing
        },
        onLoad() {
          
        },
        onLoad() {
            // 获取swiper height
            uni.getSystemInfo({
                success: (res) => {
                    this.swiperheight = res.windowHeight - uni.upx2px(100);
                }
            })
        },
        data() {
            return {
                swiperheight: null,
                tabIndex: 0,
                
               newsList:[
                   {
                       loadtext:"下拉加载更多",
                     list:[
                         {
                                 userpic:"../../static/demo/userpic/12.jpg",
                                 username:"ttt",
                                 age:20,
                                 sex:0,
                                 isguanzhu:true
                                 
                         },
                         {
                                 userpic:"../../static/demo/userpic/12.jpg",
                                 username:"aaa",
                                 age:20,
                                 sex:0,
                                 isguanzhu:false
                                 
                         },
                         {
                                 userpic:"../../static/demo/userpic/12.jpg",
                                 username:"aaa",
                                 age:21,
                                 sex:1,
                                 isguanzhu:false
                                 
                         },
                     ]
                   },
                   {
                       loadtext:"下拉加载更多",
                     list:[
                         {
                                 userpic:"../../static/demo/userpic/12.jpg",
                                 username:"ttt",
                                 age:20,
                                 sex:0,
                                 isguanzhu:true
                                 
                         },
                         {
                                 userpic:"../../static/demo/userpic/12.jpg",
                                 username:"aaa",
                                 age:20,
                                 sex:0,
                                 isguanzhu:false
                                 
                         },
                         {
                                 userpic:"../../static/demo/userpic/12.jpg",
                                 username:"aaa",
                                 age:21,
                                 sex:1,
                                 isguanzhu:false
                                 
                         },
                     ]
                   },
                   {
                       loadtext:"下拉加载更多",
                     list:[
                         {
                                 userpic:"../../static/demo/userpic/12.jpg",
                                 username:"ttt",
                                 age:20,
                                 sex:0,
                                 isguanzhu:true
                                 
                         },
                         {
                                 userpic:"../../static/demo/userpic/12.jpg",
                                 username:"aaa",
                                 age:20,
                                 sex:0,
                                 isguanzhu:false
                                 
                         },
                         {
                                 userpic:"../../static/demo/userpic/12.jpg",
                                 username:"aaa",
                                 age:21,
                                 sex:1,
                                 isguanzhu:false
                                 
                         },
                     ]
                   }
               ],
                tabBars: [{
                        name: "互关",
                        id: "huguan",
                        num:10
                    },
                    {
                        name: "关注",
                        id: "follow",
                        num:10
                    },
                    {
                        name: "粉丝",
                        id: "fensi",
                        num:10
                    },

                ],
            }
        },
        methods: {
            // 上拉加载
            loadmore(index) {
                if (this.newsList[index].loadtext != "上拉加载更多") {
                    return;
                }
                // 修改状态
                this.newsList[index].loadtext = "上拉加载更多"
                // 获取数据

                // 获取成功
                this.newsList[index].loadtext = "加载中..."
                // this.newsList[index].loadtext = "没有数据啦！"
                setTimeout(() => {
                    let obj =  {
                                 userpic:"../../static/demo/userpic/12.jpg",
                                 username:"aaa",
                                 age:21,
                                 sex:1,
                                 isguanzhu:false
                                 
                         }
                    // 添加数据
                    this.newsList[index].list.push(obj)
                    this.newsList[index].loadtext = "上拉加载更多"
                }, 500)

            },
            tabtap(index) {
                this.tabIndex = index
            },
            tabChange(e) {
                this.tabIndex = e.detail.current;
            },
        },
        // 监听导航按钮
        onNavigationBarButtonTap(e) {
            if (e.index === 0) {
              
                uni.navigateBack({
                    delte: 1
                });

            }
        }
    }
</script>

<style lang="scss" scoped>

</style>
