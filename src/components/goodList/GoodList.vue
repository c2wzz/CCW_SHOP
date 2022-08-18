<template>
    <view class="goods_list">
        <view class="goods_item" v-for="item in hotgoods" :key="item.goods_id">
            <image :src="item.image_src" mode="scaleToFill" />
            <view class="price">
                <text>￥?????</text>
                <text>{{ item.name }}</text>
            </view>
            <view>
                <text>华为荣耀6Plus 16G双4G版</text>
            </view>
        </view>
    </view>
</template>

<script>
export default {
    props:[hotgoods],
    name:'GoodList',
    data(){
        return{
        }
    },
}
</script>

<style lang="scss">
.goods_list {
    padding: 0 15rpx;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    .goods_item {
        background-color: #fff;
        width: 355rpx;
        margin: 10rpx 0;
        padding: 15rpx;
        box-sizing: border-box; // 防止padding撑大盒子导致图片换行。

        image {
            width: 80%;
            height: 150px;
            display: block;
            margin: 0 auto;
        }

        .price {
            color: $uni-shop-color;
            font-size: 36rpx;

            text:nth-child(2) {
                color: #ccc;
                font-size: 28rpx;
                margin-left: 7rpx;
                text-decoration: line-through;
            }
        }

        .name {
            font-size: 28rpx;
            line-height: 50rpx;
            padding-bottom: 15rpx;
            padding-top: 10rpx;
        }
    }

}
</style>