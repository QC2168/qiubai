<template>
	<view class="search">
        <template v-if="list.length!==0">
            <block v-for="(item,index) in list" :key="index">
		    <index-list :item="item" :index="index"></index-list>
            <!-- 上拉加载-->
            <load-more :loadtext="loadtext"></load-more>
		</block>
        </template>
	<template v-else-if="issearch && list.length<1">
	 <no-thing></no-thing>
	</template>
	</view>
</template>

<script>
        import indexList from "../../components/index/index-list.vue"
        import noThing from "../../components/common/no-thing.vue"
        	import loadMore from "../../components/common/load-more.vue";
	export default {
        components:{
            indexList,
            noThing,
            loadMore
        },
		data() {
			return {
                issearch:false,
                loadtext: "上拉加载更多",
				list:[],
                searchtext:""
			};
		},
        methods:{
            getdata(){
                //请求服务器
                let searchtext=this.searchtext
                uni.showLoading();
                setTimeout(()=>{
                    let arr=[
                        {
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
                        }
                    ];
                    this.list=arr;
                    uni.hideLoading();
                },1000)
              
            },
            loadmore() {
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
                    this.list.push(obj)
                    this.loadtext = "上拉加载更多"
                         this.issearch=true;
                }, 500)
            
            },
            // 监听原生标题导航按钮点击事件  搜索按钮
            onNavigationBarButtonTap(e){
        
               if(e.index===0){
                   uni.navigateBack({
                       delta:1
                   });
               }
            },
            
            // 监听搜索框
            onNavigationBarSearchInputChanged(e){
                // e.text
                // if(e.text) this.getdata(e.text);
               
            },
            // 监听点击键盘的确定
            onNavigationBarSearchInputConfirmed(){
                // e.text
                     if(e.text) this.getdata();
            }
            
        },
        // 监听下拉刷新
        onPullDownRefresh() {
        	this.getdata();
        	uni.stopPullDownRefresh();
        },
        //监听页面触底事件
        onReachBottom(){
            this.loadmore()
        }
	}
</script>

<style lang="scss">

</style>
