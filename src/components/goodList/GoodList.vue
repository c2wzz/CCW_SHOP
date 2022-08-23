<template>
    <view class="goods_list">
        <view class="goods_item" v-for="item in hotgoods" :key="item.id" @click="navigator(item.id)">
            <image :src="item.img_url" mode="scaleToFill" />
            <view class="price">
                <text>{{item.sell_price}}</text>
                <text>{{ item.market_price }}</text>
            </view>
            <view>
                <text>{{item.zhaiyao}}</text>
            </view>
        </view>
    </view>
</template>

<script>
export default {
    props: ['hotgoods'],
    methods:{
        navigator (id){
            this.$emit('goodsItemClick',id)
        }
    }
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