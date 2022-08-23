<template>
    <view class="detail">
        <!-- 轮播图 -->
        <swiper
            indicator-dots
            autoplay
            circular
        >
            <swiper-item v-for="(item,index) in swipers" :key="index">
                <image :src="item.src"/>
            </swiper-item>
        </swiper>
    </view>
</template>

<script>
export default {
    data() {
        return {
            id: 0,
            swipers:[]
        }
    },
    methods: {
        async getSwiper() {
            const res = await this.$myRequest({
                url: '/api/getthumimages/'+this.id
            })
            this.swipers = res.data.message
        }
    },
    onLoad(options) {
        this.id = options.id
        this.getSwiper()
    }
}
</script>

<style lang="scss">
.detail{
    swiper {
		width: 750rpx;
        height: 600rpx;
		image {
			height: 100%;
			width: 100%;
		}
	}
}
</style>