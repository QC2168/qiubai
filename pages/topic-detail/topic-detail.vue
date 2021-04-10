<template>
    <view>
        <!-- 话题介绍 -->
        <topic-info :item="topicInfo"></topic-info>
        <!-- tab切换 -->
        <swiper-tab-head srcollStyle="border-bottom:0;" scrollItemStyle="width:50%" @tabtap="tabtap" :tabBars="tabBars"
            :tabIndex="tabIndex"></swiper-tab-head>
        <view class="topic-detail-list">
            <block v-for="(item,index) in tablist" :key="index">
            				<template v-if="tabIndex==index">
            					<!-- 列表 -->
            					<block v-for="(list,listindex) in item.list" :key="listindex">
            						<common-list :item="list" :index="listindex"></common-list>
            					</block>
            					<!-- 上拉加载 -->
            					<load-more :loadtext="item.loadtext"></load-more>
            				</template>
            			</block>
        </view>
    </view>
</template>

<script>
    import topicInfo from "../../components/topic/topic-info.vue"
    import swiperTabHead from "../../components/index/swiper-tab-head.vue"
    import commonList from "../../components/common/common-list.vue"
    import loadMore from "../../components/common/load-more.vue"
    export default {
        components: {
            topicInfo,
            swiperTabHead,
            commonList,
            loadMore
        },
        data() {
            return {
                tabIndex: 0,
                tabBars: [{
                        name: "默认",
                        id: "default"
                    },
                    {
                        name: "最新",
                        id: "new"
                    }

                ],
                topicInfo: {
                    titlepic: "../../static/demo/topicpic/13.jpeg",
                    title: "#title#",
                    desc: "大大大大大大",
                    totalnum: 100,
                    todaynum: 100

                },
                tablist: [{
                        loadtext: "上拉加载更多",
                        list: [{
                            userpic: "../../static/demo/datapic/10.jpg",
                            username: "username",
                            sex: 0,
                            age: 25,
                            isFollow: false,
                            title: "我的title",
                            video: false,
                            share: false,
                            path: "广东揭阳",
                            sharenum: 20,
                            commentnum: 30,
                            goodnum: 22
                        }, ]
                    },
                    {
                        loadtext: "上拉加载更多",
                        list: [{
                            userpic: "../../static/demo/datapic/10.jpg",
                            username: "username",
                            sex: 0,
                            age: 25,
                            isFollow: false,
                            title: "我的title",
                            video: false,
                            share: false,
                            path: "广东揭阳",
                            sharenum: 20,
                            commentnum: 30,
                            goodnum: 22
                        }, {
                            userpic: "../../static/demo/datapic/10.jpg",
                            username: "username",
                            sex: 0,
                            age: 25,
                            isFollow: false,
                            title: "我的title",
                            video: false,
                            share: false,
                            path: "广东揭阳",
                            sharenum: 20,
                            commentnum: 30,
                            goodnum: 22
                        }, {
                            userpic: "../../static/demo/datapic/10.jpg",
                            username: "username",
                            sex: 0,
                            age: 25,
                            isFollow: false,
                            title: "我的title",
                            video: false,
                            share: false,
                            path: "广东揭阳",
                            sharenum: 20,
                            commentnum: 30,
                            goodnum: 22
                        }, {
                            userpic: "../../static/demo/datapic/10.jpg",
                            username: "username",
                            sex: 0,
                            age: 25,
                            isFollow: false,
                            title: "我的title",
                            video: false,
                            share: false,
                            path: "广东揭阳",
                            sharenum: 20,
                            commentnum: 30,
                            goodnum: 22
                        }, ]
                    }
                ],

            }
        },
        //下拉刷新  
        onPullDownRefresh() {
          this.getdata()
        },
        onReachBottom () {
            // 上啦加载
            this.loadmore()
        },
        methods: {
            getdata(){
              //上拉刷新事件
              let obj = {
                  userpic: "../../static/demo/datapic/10.jpg",
                  username: "12333",
                  sex: 0,
                  age: 25,
                  isFollow: false,
                  title: "我的1222",
                  video: false,
                  share: false,
                  path: "广东揭阳",
                  sharenum: 20,
                  commentnum: 30,
                  goodnum: 22
              }
              
              //关闭刷新
                setTimeout(()=>{
                  this.tablist[this.tabIndex].list=obj
                   uni.stopPullDownRefresh();
                },1000)
            },
            tabtap(index) {
                this.tabIndex = index
            },
            loadmore() {
             
                    if(this.tablist[this.tabIndex].loadtext != "上拉加载更多") {
                        return;
                    }
                    // 修改状态
                    this.tablist[this.tabIndex].loadtext = "上拉加载更多"
                    // 获取数据
                                
                    // 获取成功
                     this.tablist[this.tabIndex].loadtext = "加载中..."
                    // this.newsList[index].loadtext = "没有数据啦！"
                    setTimeout(() => {
                        let obj = {
                            userpic: "../../static/demo/datapic/10.jpg",
                            username: "user",
                            sex: 0,
                            age: 25,
                            isFollow: false,
                            title: "title",
                            video: false,
                            share: false,
                            path: "广东揭阳",
                            sharenum: 20,
                            commentnum: 30,
                            goodnum: 22
                        }
                        // 添加数据
                        this.tablist[this.tabIndex].list.push(obj)
                        this.tablist[this.tabIndex].loadtext = "上拉加载更多"
                        }, 500)                                    
            },
        }
    }
</script>

<style scoped lang="scss">

</style>
