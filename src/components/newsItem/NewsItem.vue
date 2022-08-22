<template>
    <view>
        <view class="news_item" @click="navigator(item.id)" v-for="(item) in newslist" :key="item.id">
            <image :src="item.img_url" />
            <view class="right">
                <view class="tit">{{ item.title }}</view>
                <view class="info">
                    <text>发表时间:{{ item.add_time | formatDate }}</text>
                    <text>浏览:{{ item.click }}</text>
                </view>
            </view>
        </view>
    </view>

</template>

<script>
export default {
    props: ['newslist'],
    filters: {
        formatDate(date) {
            const nDate = new Date(date)
            const year = nDate.getFullYear()
            // vue计算月份时从0开始的，1-12月=0-11月，所以需要 + 1
            const month = (nDate.getMonth()+1).toString().padStart(2, 0)
            // getDay是获取星期几的，这里获取具体几号要用getDate
            const day = nDate.getDate().toString().padStart(2, 0)
            return year + '-' + month + '-' + day
        }
    },
    methods:{
        navigator(id){
            this.$emit('itemClick',id)
        }
    },
    date() {
        return {

        }
    },
}
</script>

<style lang="scss">
.news_item {
    display: flex;
    padding: 10rpx 20rpx;
    border-bottom: 1px solid $uni-shop-color;

    image {
        width: 200rpx;
        min-width: 200rpx;
        max-width: 200rpx;
        height: 150rpx;
        max-height: 150rpx;
    }

    .right {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        margin-left: 30rpx;

        .tit {
            font-size: 33rpx;
        }

        .info {
            text {
                font-size: 20rpx;
            }
            text:nth-child(2) {
                    margin-left: 60rpx
            }
        }
    }

}
</style>