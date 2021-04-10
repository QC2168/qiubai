<template>
	<view>
		<swiper-tab-head 
        @tabtap="tabtap" 
        :tabBars="tabBars" 
        :tabIndex="tabIndex"
        ></swiper-tab-head>
        <view class="uni-tab-bar">
            <swiper class="swiper-box" :style="{height:swiperheight+'px'}" :current="tabIndex" @change="tabChange">
                <swiper-item v-for="(items,index) in newsList" :key="index">
                    <scroll-view scroll-y class="list" @scrolltolower="loadmore(index)">
                        <template v-if="items.list.length!==0">
                            <view>
                                <!-- 话题列表-->
                                <view class="topic-view">
                                    <block v-for="(item,index1) in items.list" :key="index1">
                                           <topic-list :item="item" :index="index1"></topic-list>
                                    </block>
                                </view>
                           
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
    import noThing from "../../components/common/no-thing.vue"
    import loadMore from "../../components/common/load-more.vue"
           import topicList from "../../components/news/topic-list.vue"
	export default {
        components: {
noThing,loadMore,topicList,
            swiperTabHead,

        },
		data() {
			return {
                
                 swiperheight: null,
           tabIndex:0,
           newsList: [{
                   loadtext: "上拉加载更多",
                   list: [{
                            titlepic:"../../static/demo/topicpic/13.jpeg",
                            title:"#话题名称#",
                            desc:"我的话题描述",
                            totalnum:"10",
                            todaynum:"5",
                        },{
                            titlepic:"../../static/demo/topicpic/13.jpeg",
                            title:"#话题名称2#",
                            desc:"我的话题描述2",
                            totalnum:"10",
                            todaynum:"5",
                        },]
               },
               {
                   loadtext: "上拉加载更多",
                   list: [{
                            titlepic:"../../static/demo/topicpic/13.jpeg",
                            title:"#话题名称#",
                            desc:"我的话题描述",
                            totalnum:"10",
                            todaynum:"5",
                        },{
                            titlepic:"../../static/demo/topicpic/13.jpeg",
                            title:"#话题名称2#",
                            desc:"我的话题描述2",
                            totalnum:"10",
                            todaynum:"5",
                        },{
                            titlepic:"../../static/demo/topicpic/13.jpeg",
                            title:"#话题名称#",
                            desc:"我的话题描述",
                            totalnum:"10",
                            todaynum:"5",
                        },{
                            titlepic:"../../static/demo/topicpic/13.jpeg",
                            title:"#话题名称2#",
                            desc:"我的话题描述2",
                            totalnum:"10",
                            todaynum:"5",
                        },{
                            titlepic:"../../static/demo/topicpic/13.jpeg",
                            title:"#话题名称#",
                            desc:"我的话题描述",
                            totalnum:"10",
                            todaynum:"5",
                        },{
                            titlepic:"../../static/demo/topicpic/13.jpeg",
                            title:"#话题名称2#",
                            desc:"我的话题描述2",
                            totalnum:"10",
                            todaynum:"5",
                        },]
               },
               {
                   loadtext: "上拉加载更多",
                   list: []
               },
               {
                   loadtext: "上拉加载更多",
                   list: []
               },
               {
                   loadtext: "上拉加载更多",
                   list: []
               },
               {
                   loadtext: "上拉加载更多",
                   list: []
               },
           ],
				tabBars: [{
				        name: "关注",
				        id: "guanzhu"
				    },
				    {
				        name: "推荐",
				        id: "tuijian"
				    },
				    {
				        name: "体育",
				        id: "tiyu"
				    },
				    {
				        name: "热点",
				        id: "redian"
				    },
				    {
				        name: "体育",
				        id: "tiyu"
				    },
				    {
				        name: "娱乐",
				        id: "yule"
				    }
				]
			}
		},
		methods: {
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
                        let obj = {
                            titlepic:"../../static/demo/topicpic/13.jpeg",
                            title:"#话题名称#",
                            desc:"我的话题描述",
                            totalnum:"10",
                            todaynum:"5",
                        }
                        // 添加数据
               this.newsList[index].list.push(obj)
               this.newsList[index].loadtext = "上拉加载更多"
                    }, 500)
                                
           
               
            },
            tabChange(e) {
                this.tabIndex = e.detail.current;
            },
			tabtap(index) {
			    this.tabIndex = index
			},
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

<style>
.topic-view{
    padding: 0 20upx;
}
</style>
