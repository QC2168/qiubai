<template>
    <view class="detail">
        <detail-info :item="detail"></detail-info>

        <view class="u-comment-title">最新评论 {{comment.count}}</view>
        <view class="uni-comment u-comment">
            <block v-for="(item,index) in comment.list" :key="index">
                <comment-list :item="item" :index="index"></comment-list>
            </block>
        </view>
        <view style="height: 120upx;"></view>
        <!-- 输入框 -->
        <user-chat-bottom @submit="submit"></user-chat-bottom>

        <!-- 分享 -->
        <more-share :show="shareshow" @clickshow="show()"></more-share>
        
    </view>
</template>

<script>
    import detailInfo from "../../components/detail/detail-info.vue";
    import userChatBottom from "../../components/user-chat/user-chat-bottom.vue";
    import time from "../../common/time.js";
    import commentList from "../../components/detail/comment-list.vue";
    import moreShare from "../../components/common/more-share.vue";
    export default {
        components: {
            detailInfo,
            commentList,
            userChatBottom,
            moreShare
        },
        data() {
            return {
                shareshow:false,
                comment: {
                    count: 20,
                    list: []
                },
                detail: {
                    userpic: "../../static/demo/userpic/12.jpg",
                    username: "哈哈",
                    sex: 0, //0 男 1 女
                    age: 25,
                    isguanzhu: false,
                    title: "我是标题",
                    titlepic: "../../static/demo/datapic/13.jpg",
                    morepic: [
                        "../../static/demo/datapic/13.jpg", 
                        "../../static/demo/datapic/14.jpg",
                        "../../static/demo/datapic/15.jpg"
                    ],
                    video: false,
                    share: false,
                    path: "深圳 龙岗",
                    sharenum: 20,
                    commentnum: 30,
                    goodnum: 20
                },
            }
        },
        onLoad(e) {
            this.initdata(JSON.parse(e.detailData));
            this.getcomment();
        },
        // 监听导航右边按钮
        onNavigationBarButtonTap(e) {
            if (e.index == 0) {
               this.show();
            }
        },
        methods: {
            show(){
                this.shareshow=!this.shareshow
            },
            submit() {
                let obj = {
                    id: 1,
                    fid: 0,
                    userpic: "https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
                    username: "小猫咪",
                    time: time.gettime.gettime(new Date().getTime()),
                    data: "支持国产，支持DCloud!",
                }
                this.comment.list.push(obj)
            },

            // 获取评论
            getcomment() {
                let arr = [
                    // 一级评论
                    {
                        id: 1,
                        fid: 0,
                        userpic: "https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
                        username: "小猫咪",
                        time: "1555400035",
                        data: "支持国产，支持DCloud!",
                    },
                    // 子级评论
                    {
                        id: 2,
                        fid: 1,
                        userpic: "https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
                        username: "小猫咪",
                        time: "1555400035",
                        data: "支持国产，支持DCloud!",
                    },
                    {
                        id: 3,
                        fid: 1,
                        userpic: "https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
                        username: "小猫咪",
                        time: "1555400035",
                        data: "支持国产，支持DCloud!",
                    },
                    {
                        id: 4,
                        fid: 0,
                        userpic: "https://img-cdn-qiniu.dcloud.net.cn/uniapp/images/uni@2x.png",
                        username: "小猫咪",
                        time: "1555400035",
                        data: "支持国产，支持DCloud!",
                    },
                ];
                for (let i = 0; i < arr.length; i++) {
                    arr[i].time = time.gettime.gettime(arr[i].time);
                }
                this.comment.list = arr;
            },
            // 初始化数据
            initdata(obj) {
                // 修改窗口标题
                uni.setNavigationBarTitle({
                    title: obj.title
                });
            }
        }
    }
</script>

<style scoped lang="scss">
    .detail {
        .u-comment {
            padding: 0 20upx;
        }

        .u-comment-title {
            padding: 20upx;
            font-size: 30upx;
            font-weight: bold;
        }

      
    }


    /* 分享 */
    // .more-share-model {
    //     background: rgba(51, 51, 51, 0.49);
    //     position: fixed;
    //     top: 0;
    //     left: 0;
    //     right: 0;
    //     bottom: 0;
    //     z-index: 100;
    // }

    // .more-share {
    //     position: fixed;
    //     z-index: 110;
    //     bottom: 0;
    //     left: 0;
    //     right: 0;
    //     background: #FFFFFF;
    // }

    // .more-share-title,
    // .more-share-bottom {
    //     font-size: 32upx;
    //     padding: 25upx;
    // }

    // .more-share-body {
    //     white-space: nowrap;
    //     width: 100%;
    //     height: 200upx;
    //     border-bottom: 1upx solid #EEEEEE;
    //     display: flex !important;
    //     line-height: 200upx !important;
    // }

    // .more-share-item {
    //     width: 25%;
    //     display: inline-flex;
    //     justify-content: center;
    //     align-items: center;
    //     flex-direction: column;
    //     height: 100%;
    // }

    // .more-share-item>view:first-child {
    //     width: 100upx;
    //     height: 100upx;
    //     border-radius: 100%;
    //     font-size: 55upx;
    //     color: #FFFFFF;
    // }

    // .more-share-item>view:last-child {
    //     color: #7A7A7A;
    // }

    // .more-share-hover {
    //     background: #EEEEEE;
    // }

    // .more-share-wx {
    //     background: #2AD19B;
    // }

    // .more-share-pyq {
    //     background: #514D4C;
    // }

    // .more-share-wb {
    //     background: #EE5E5E;
    // }

    // .more-share-qq {
    //     background: #4A73BA;
    // }
</style>
