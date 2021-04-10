<template>
    <view>

        <swiper-tab-head @tabtap="tabtap" :tabBars="tabBars" :tabIndex="tabIndex"></swiper-tab-head>
        <view class="uni-tab-bar">
            <swiper class="swiper-box" :style="{height:swiperheight+'px'}" :current="tabIndex" @change="tabChange">
                <swiper-item v-for="(items,index) in newsList" :key="index">
                    <scroll-view scroll-y class="list" @scrolltolower="loadmore(index)">
                        <template v-if="items.list.length!==0">
                            <view>
                                <!-- 图文列表-->
                                <block v-for="(item,index1) in items.list" :key="index1">
                                    <index-list :item="item" :index="index1"></index-list>
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
    import indexList from "../../components/index/index-list.vue"
    import swiperTabHead from "../../components/index/swiper-tab-head.vue"
    import loadMore from "../../components/common/load-more.vue"
    import noThing from "../../components/common/no-thing.vue"
    export default {
        components: {
            indexList,
            swiperTabHead,
            loadMore,
            noThing
        },
        data() {
            return {
                swiperheight: null,
                tabIndex: 0,

                list: [

                ],
                newsList: [{
                        loadtext: "上拉加载更多",
                        list: [{

                            userpic: "../../static/demo/userpic/12.jpg",
                            username: "QC2125",
                            isFollow: false,
                            title: "this is content",
                            type: "img", // 类型
                            titlePic: "../../static/demo/datapic/11.jpg",
                            playCount: 20000,
                            long: "2:47",
                            infoCount: {
                                index: 0, //没有操作，1顶  2踩
                                dingCount: 11,
                                caiCount: 11,
                            },
                            commentCount: 1,
                            shareCount: 2
                        }]
                    },
                    {
                        loadtext: "上拉加载更多",
                        list: [{
                            userpic: "../../static/demo/userpic/12.jpg",
                            username: "QC2125",
                            isFollow: false,
                            title: "this is content",
                            type: "img", // 类型
                            titlePic: "../../static/demo/datapic/11.jpg",
                            playCount: 20000,
                            long: "2:47",
                            infoCount: {
                                index: 2, //没有操作，1顶  2踩
                                dingCount: 11,
                                caiCount: 11,
                            },
                            commentCount: 1,
                            shareCount: 2
                        }, {

                            userpic: "../../static/demo/userpic/12.jpg",
                            username: "QC2125",
                            isFollow: false,
                            title: "this is content",
                            type: "img", // 类型
                            titlePic: "../../static/demo/datapic/11.jpg",
                            playCount: 20000,
                            long: "2:47",
                            infoCount: {
                                index: 0, //没有操作，1顶  2踩
                                dingCount: 11,
                                caiCount: 11,
                            },
                            commentCount: 1,
                            shareCount: 2
                        }, {

                            userpic: "../../static/demo/userpic/12.jpg",
                            username: "QC2125",
                            isFollow: false,
                            title: "this is content",
                            type: "img", // 类型
                            titlePic: "../../static/demo/datapic/11.jpg",
                            playCount: 20000,
                            long: "2:47",
                            infoCount: {
                                index: 2, //没有操作，1顶  2踩
                                dingCount: 11,
                                caiCount: 11,
                            },
                            commentCount: 1,
                            shareCount: 2
                        }]
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
        onLoad() {
            // 获取swiper height
            uni.getSystemInfo({
                success: (res) => {
                    this.swiperheight = res.windowHeight - uni.upx2px(100);
                }
            })
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
                    let obj = {
                        userpic: "../../static/demo/userpic/12.jpg",
                        username: "QC2125",
                        isFollow: false,
                        title: "this is content",
                        type: "img", // 类型
                        titlePic: "../../static/demo/datapic/11.jpg",
                        playCount: 20000,
                        long: "2:47",
                        infoCount: {
                            index: 1, //没有操作，1顶  2踩
                            dingCount: 11,
                            caiCount: 11,
                        },
                        commentCount: 1,
                        shareCount: 2
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
            onNavigationBarSearchInputClicked() {
                uni.navigateTo({
                    url: "../search/search"
                })
            },
            onNavigationBarButtonTap(e) {
                if (e.index === 1) {
                    uni.navigateTo({
                        // push add input
                        url: "../add-input/add-input"
                    })
                }
            },

        }
    }
</script>

<style scoped lang="scss">

</style>
