<template>
    <view class="news">
        <!-- 自定义导航栏 -->
        <news-nav-bar @changeTabIndex="changeTabIndex" @toAdd="toAdd" :tabIndex="tabIndex" :tabList="tabList"></news-nav-bar>


        <!-- 列表 -->
     <view class="uni-tab-bar">
         <swiper class="swiper-box" :style="{height:swiperheight+'px'}" :current="tabIndex" @change="tabChange">
             <swiper-item>
         
                            <scroll-view scroll-y class="list" @scrolltolower="loadmore('followList')">
                           <block v-for="(item,index) in followList.list" :key="index">
                                <common-list :item="item" ></common-list>
                            </block>
                            <!-- 上拉加载-->
                            <load-more :loadtext="followList.loadtext"></load-more>
                         </scroll-view>

             </swiper-item>
             <swiper-item>
         <scroll-view scroll-y class="list" @scrolltolower="loadmore('followList')">
                         <view>
                            <!-- 搜索框 -->
                            <view class="search-input">
                                <input placeholder-class="icon iconfont icon-sousuo topic-search" placeholder="搜索内容" class="uni-input" value="" />
                            </view>
                            <!-- 轮播图 -->
                            <swiper class="topic-swiper" :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
                                <swiper-item v-for="(item,index) in topic.swiper" :key="index">
                                    <image :src="item.src" lazy-load mode="widthFix"></image>
                                </swiper-item>
                            </swiper>
                            <!-- 热门分类 -->
                            <topic-nav :nav="topic.nav"></topic-nav>
                            <!-- 最新更新 -->
                            <block v-for="(item,index) in topic.list" :key="index">
                                <topic-list :item="item" :index="index"></topic-list>
                            </block>
                         </view>
                         </scroll-view>
             </swiper-item>
         </swiper>
     </view>   



    </view>

</template>

<script>
    import uniNavBar from "../../components/uni-nav-bar/uni-nav-bar.vue"
    import commonList from "../../components/common/common-list.vue"
    import newsNavBar from "../../components/news/news-nav-bar.vue"
    import topicNav from "../../components/news/topic-nav.vue"
        import loadMore from "../../components/common/load-more.vue"
        import topicList from "../../components/news/topic-list.vue"
    export default {
        components: {
            uniNavBar,commonList,newsNavBar,loadMore,topicNav,topicList
        },
        data() {
            return {
                 swiperheight: null,
                tabIndex: 1,
                topic:{
                    swiper:[
                        {src:"../../static/demo/banner1.jpg"},
                        {src:"../../static/demo/banner1.jpg"},
                        {src:"../../static/demo/banner1.jpg"},
                        {src:"../../static/demo/banner1.jpg"}
                    ],
                    nav:[
                        {name:"最新"},
                        {name:"打卡"},
                        {name:"游戏"},
                        {name:"情感"},
                        {name:"故事"},
                        {name:"喜爱"},
                    ],
                    list:[
                        {
                            titlepic:"../../static/demo/topicpic/13.jpeg",
                            title:"#话题名称#",
                            desc:"我的话题描述",
                            totalnum:"10",
                            todaynum:"5",
                        },
                        {
                            titlepic:"../../static/demo/topicpic/13.jpeg",
                            title:"#话题名称2#",
                            desc:"我的话题描述2",
                            totalnum:"110",
                            todaynum:"4",
                        },
                    ]
                },
                tabList: [{
                        name: "关注",
                        id: "gz"
                    },
                    {
                        name: "话题",
                        id: "ht"
                    }
                ],
                followList:{
                    loadtext:"上拉加载更多",
                    list:[
                    //文字列表
                    {
                        userpic:"../../static/demo/datapic/10.jpg",
                        username:"username",
                        sex:0,
                        age:25,
                        isFollow:false,
                        title:"我的title",
                        video:false,
                        share:false,
                        path:"广东揭阳",
                        sharenum:20,
                        commentnum:30,
                        goodnum:22
                    },
                    // 图文列表
                    {
                        userpic:"../../static/demo/datapic/10.jpg",
                        username:"username",
                        sex:0,
                        age:25,
                        isFollow:false,
                        title:"我的title",
                        titlepic:"../../static/demo/banner2.jpg",
                        video:false,
                        share:false,
                        path:"广东揭阳",
                        sharenum:20,
                        commentnum:30,
                        goodnum:22
                    },
                    // 视频
                    {
                        userpic:"../../static/demo/datapic/10.jpg",
                        username:"username",
                        sex:0,
                        age:25,
                        isFollow:false,
                        title:"我的title",
                        titlepic:"../../static/demo/banner2.jpg",
                        video:{
                            looknum:"22W",
                            long:"2:17"
                        },
                        share:false,
                        path:"广东揭阳",
                      sharenum:20,
                      commentnum:30,
                      goodnum:22
                    },
                    // 分享
                    {
                        userpic:"../../static/demo/datapic/10.jpg",
                        username:"username",
                        sex:0,
                        age:25,
                        isFollow:false,
                        title:"我的title",
                        titlepic:"",
                        video:false,
                        share:{
                            title:"kkk1",
                            titlepic:"../../static/demo/banner2.jpg"
                        },
                        path:"广东揭阳",
                       sharenum:20,
                       commentnum:30,
                       goodnum:22
                    },
                ]
                }
            }
        },
        methods: {
            //下拉加载
            loadmore(index) {
                if(index==="followList"){
                    if(this.followList.loadtext != "上拉加载更多") {
                        return;
                    }
                    // 修改状态
                    this.followList.loadtext = "上拉加载更多"
                    // 获取数据
                                
                    // 获取成功
                     this.followList.loadtext = "加载中..."
                    // this.newsList[index].loadtext = "没有数据啦！"
                    setTimeout(() => {
                        let obj = {
                                userpic:"../../static/demo/datapic/10.jpg",
                                username:"username",
                                sex:0,
                                age:25,
                                isFollow:false,
                                title:"我的title",
                                titlepic:"",
                                video:false,
                                share:{
                                    title:"kkk1",
                                    titlepic:"../../static/demo/banner2.jpg"
                                },
                                path:"广东揭阳",
                               sharenum:20,
                               commentnum:30,
                               goodnum:22
                         }
                        // 添加数据
                        this.followList.list.push(obj)
                        this.followList.loadtext = "上拉加载更多"
                    }, 500)
                                
                }
                return;
               
            },
            tabtap(index) {
                this.tabIndex = index
            },
            tabChange(e) {
                this.tabIndex = e.detail.current;
            },
            changeTabIndex(index) {
                this.tabIndex = index;
            },
            toAdd() {
                uni.navigateTo({
                    url: "../add-input/add-input"
                })
            }
        },
        onLoad() {
            // 获取swiper height
            uni.getSystemInfo({
                success: (res) => {
                    this.swiperheight = res.windowHeight - uni.upx2px(100);
                }
            })
        },
    }
</script>

<style scoped lang="scss">

.search-input{
    input{
        background-color: #EEEEEE;
        padding: 20upx;
        border-radius: 10upx;
        
    }
    .topic-search{
         display: flex;
         justify-content: center;
         font-size: 27upx;
    }
}
.topic-swiper{
    padding: 0 20upx 20upx 20upx;
    image{
        width: 100%;
        border-radius: 10upx;
        
    }
}

    

    
</style>
