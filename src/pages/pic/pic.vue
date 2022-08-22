<template>
    <view class="pics">
        <scroll-view scroll-y class="left">
            <view 
                :class="active === index ? 'active' : ''" 
                v-for="(item, index) in cates" 
                :key="item.id"
                @click="leftClick(index, item.id)"
            >
                {{ item.title }}
            </view>
        </scroll-view>
        <scroll-view class="right" scroll-y >
            <view class="item" v-for="item in secondData" :key='item.id'>
                <image @click="previewImg(item.img_url)" :src="item.img_url" />
                <text>{{ item.title }}</text>
            </view>
        </scroll-view>
    </view>
</template>

<script>
export default {
    data() {
        return {
            cates: [],
            active: 0,
            secondData: []
        }
    },
    onLoad() {
        this.getPicCate()
    },
    methods: {
        async getPicCate() {
            const res = await this.$myRequest({
                url: '/api/getimgcategory'
            })
            this.cates = res.data.message
        },
        async leftClick(index, id) {
            this.active = index;
            // 获取右侧数据
            const res = await this.$myRequest({
                url: '/api/getimages/' + id
            })
            this.secondData = res.data.message
            // 默认进入页面时载入第一条图片信息
            // this.leftClick(0,this.cates[0].id)
        },
        previewImg(current){
            const urls = this.secondData.map(item=>{
                return item.img_url
            })
            uni.previewImage({
                current,
                urls
            })
        }
    }

}
</script>
<style lang="scss">
page {
    height: 100%;
}
.pics {
    height: 100%;
    display: flex;
    .left {
        width: 200rpx;
        height: 100%;
        border-right: solid 1px #eee;
        border-top: solid 1px #eee;

        view {
            height: 120rpx;
            line-height: 120rpx;
            color: #333;
            text-align: center;
            font-size: 30rpx;
        }

        .active {
            background-color: $uni-shop-color;
            color: #fff
        }
    }
    .right{
        width: 550rpx;
        height: 100%;
        margin: 0 auto;
        .item{
            image{
                width: 520rpx;
                height: 520rpx;
                border-radius: 5px;
            }
            text{
                font-size: 30rpx;
                line-height: 60rpx;
            }
        }
    }
}
</style>