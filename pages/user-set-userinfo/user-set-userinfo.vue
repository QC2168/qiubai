<template>
    <view class="body">
        <view class="user-set-userinfo-list u-f-ac u-f-jsb">
            <view>头像</view>
            <view class="u-f-ac">
                <image lazy-load @tap="changeimg" :src="userpic" mode="aspectFill"></image>
                <view class="icon iconfont icon-bianji1"></view>
            </view>
        </view>
        <view class="user-set-userinfo-list u-f-ac u-f-jsb">
            <view>昵称</view>
            <view class="u-f-ac">
                <input type="text" v-model="username" placeholder="黄新泓" />
                <view class="icon iconfont icon-bianji1"></view>
            </view>
        </view>
        <view class="user-set-userinfo-list u-f-ac u-f-jsb">
            <view>性别</view>
            <view class="u-f-ac" @tap="changeOne('sex')">
                <view>{{sex}}</view>
                <view class="icon iconfont icon-bianji1"></view>
            </view>
        </view>
        <view class="user-set-userinfo-list u-f-ac u-f-jsb">
            <view>生日</view>
            <view class="u-f-ac">
                <picker mode="date" :value="birthday" :start="startDate" :end="endDate" @change="bindDateChange">
                    <view>{{birthday}}</view>
                </picker>
                <view class="icon iconfont icon-bianji1"></view>
            </view>
        </view>
        <view class="user-set-userinfo-list u-f-ac u-f-jsb">
            <view>情感</view>
            <view class="u-f-ac" @tap="changeOne('qg')">
                <view>{{qg}}</view>
                <view class="icon iconfont icon-bianji1"></view>
            </view>
        </view>
        <view class="user-set-userinfo-list u-f-ac u-f-jsb">
            <view>职业</view>
            <view class="u-f-ac" @tap="changeOne('job')">
                <view>{{job}}</view>
                <view class="icon iconfont icon-bianji1"></view>
            </view>
        </view>
        <view class="user-set-userinfo-list u-f-ac u-f-jsb" >
            <view>家乡</view>
            <view class="u-f-ac">

                <view @tap="showregion">{{city.text}}</view>
                <w-picker
			mode="region"
			:defaultVal="regionDval"
			:areaCode="['33','3301','330108']"
			:hideArea="false"
			@confirm="onConfirm" 
			ref="region"
			:timeout="true"></w-picker>


                <view class="icon iconfont icon-bianji1"></view>
            </view>
        </view>
        <button @tap="submit" class="user-set-btn" type="primary">完成</button>
    </view>
</template>

<script>
    let sex = ['男', '女'];
    let qg = ['单身可撩', '已婚'];
    let job = ['IT', '前端'];
    import wPicker from "@/components/w-picker/w-picker.vue";
    export default {
        components: {
            wPicker
        },
        data() {
            return {
                regionDval:['浙江省','杭州市','滨江区'],
                userpic: "../../static/demo/userpic/11.jpg",
                username: "",
                sex: "男",
                qg: "单身可撩",
                job: "IT",
                birthday: "2002-01-25",
                city: {
                    arr: ['广东省', '揭阳市', '榕城区'],
                    text: "广东省 揭阳市 榕城区",
                    areaCode: ["44", "4452", "445202"]
                },

            };
        },
        mounted() {
             
        },
        computed: {
            startDate() {
                return this.getDate('start');
            },
            endDate() {
                return this.getDate('end');
            }
        },
        methods: {
            onCancel() {
                this.hideregion()
            },
            showregion() {
                this.$refs.region.show()
            },
            hideregion() {
                this.$refs.region.hide()

            },
            onConfirm(res) {
                this.city.arr = res.checkArr;
                this.city.text = res.result;
                this.city.areaCode = res.checkValue;

                
                this.hideregion()
                             
            },
            //修改生日
            bindDateChange: (e) => {
                this.date = e.target.value
            },
            getDate(type) {
                const date = new Date();
                let year = date.getFullYear();
                let month = date.getMonth() + 1;
                let day = date.getDate();

                if (type === 'start') {
                    year = year - 60;
                } else if (type === 'end') {
                    year = year + 2;
                }
                month = month > 9 ? month : '0' + month;;
                day = day > 9 ? day : '0' + day;
                return `${year}-${month}-${day}`;
            },
            //单列选择
            changeOne(val) {
                let arr = []
                switch (val) {
                    case 'sex':
                        arr = sex;
                        break;
                    case 'qg':
                        arr = qg;
                        break;
                    case 'job':
                        arr = job;
                        break;
                }
                uni.showActionSheet({
                    itemList: arr,
                    success: (res) => {
                        switch (val) {
                            case 'sex':
                                this.sex = arr[res.tapIndex];
                                break;
                            case 'qg':
                                this.qg = arr[res.tapIndex];
                                break;
                            case 'job':
                                this.job = arr[res.tapIndex];
                                break;
                        }
                    },
                    fail: (res) => {
                        // console.log(res.errMsg);
                    },

                });

            },
            // 修改头像
            changeimg() {

                uni.chooseImage({
                    count: 1,
                    sourceType: ['album'], //从相册选择
                    success: (res) => {
                        this.userpic = res.tempFilePaths[0];
                    }
                });
            },
            submit() {

            }
        }
    }
</script>

<style lang="scss">
    @import "../../common/form.css";

    .user-set-userinfo-list {
        padding: 20upx;
        border-bottom: 1upx solid #F4F4F4;

        view:first-child {
            font-size: 30upx;
            font-weight: bold;
            color: #9B9B9B
        }

        view:last-child {
            view:last-of-type {
                margin-left: 20upx;
                color: #9B9B9B;
            }

            input {
                text-align: right;
            }

            image {
                width: 80upx;
                height: 80upx;
                border-radius: 100%;
            }
        }
    }
</style>
