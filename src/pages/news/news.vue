<template>
  <view class="news">
    <NewsItem @itemClick="goDetail" :newslist="newslist" />
  </view>
</template>

<script>
import NewsItem from '../../components/newsItem/NewsItem'
export default {
  data() {
    return {
      newslist: [],
    };
  },
  components: { NewsItem },
   methods: {
    onLoad() {
      this.getNews();
    },
    async getNews() {
      const res = await this.$myRequest({
        url: "/api/getnewslist"
      });
      this.newslist = res.data.message;
    },
    goDetail(id) {
      console.log('触发了',id);
      uni.navigateTo({
        url:'/pages/newsDetail/NewsDetail?id='+id
      })
    }
  },
}
</script>
<style lang="scss">
.news {
  background-color: #fff;;
}
</style>