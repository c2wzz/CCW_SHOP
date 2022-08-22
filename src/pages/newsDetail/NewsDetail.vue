<template>
  <view class="new_detail">
    <text class="title">{{ details.title }}</text>
    <view class="info">
      <text>发表时间:{{ details.add_time | formatDate }}</text>
      <text>浏览:{{ details.click }}</text>
    </view>
    <view class="content">
      <rich-text :nodes="details.content"></rich-text>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      id: 0,
      details: {}
    }
  },
  filters: {
    formatDate(date) {
      const nDate = new Date(date)
      const year = nDate.getFullYear()
      // vue计算月份时从0开始的，1-12月=0-11月，所以需要 + 1
      const month = (nDate.getMonth() + 1).toString().padStart(2, 0)
      // getDay是获取星期几的，这里获取具体几号要用getDate
      const day = nDate.getDate().toString().padStart(2, 0)
      return year + '-' + month + '-' + day
    }
  },
  methods: {
    async getNewsDetail() {
      const res = await this.$myRequest({
        url: '/api/getnew/' + this.id
      })
      this.details = res.data.message[0]
    }
  },
  onLoad(options) {
    console.log(options);
    this.id = options.id;
    this.getNewsDetail();
  }
}

</script>

<style lang="scss">
.new_detail {
  font-size: 30rpx;
  padding: 0 20rpx;

  .title {
    text-align: center;
    width: 710rpx;
    display: block;
    margin: 20rpx 0;
  }

  .info {
    display: flex;
    justify-content: space-between;
  }
}
</style>