<template>
    <view class="goods-list">
        <GoodList :hotgoods="hotgoods" />
        <view class="isOver" v-if="flag">---没有更多的商品了---</view>
    </view>
</template>

<script>
import GoodList from '../../components/goodList/GoodList.vue'
export default {
    data() {
        return {
            pageindex: 1,
            hotgoods: [],
            flag:false,
        }
    },
    components: { GoodList },
    methods: {
        // 获取商品列表数据
        async getGoodsList() {
            const res = await this.$myRequest({
                url: '/api/getgoods?pageindex=' + this.pageindex
            })
            this.hotgoods = [...this.hotgoods,...res.data.message]
        }
    },
    onLoad() {
        this.getGoodsList()
    },
    onReachBottom() {
        console.log('触底了');
        if(this.hotgoods.length %10 < 10) return this.flag = true
        this.pageindex++;
        this.getGoodsList()
        console.log(this.flag);
    }
}


</script>

<style lang="scss">
.goods-list {
    background-color: #ccc;
}
.isOver {
    width: 100%;
    height: 50px;
    line-height: 50px;
    text-align: center;
    font-size: 28rpx;
}
</style>