<template>
  <view class="contact">
    <image
      class="img"
      src="https://raw.githubusercontent.com/c2wzz/CCW_SHOP/master/src/static/aboutUs.png"
      mode="scaleToFill"
    />
    <view class="info">
      <view>联系电话:400-8828-8820 (点击拨打)</view>
      <view>联系地址:福建省福州市闽侯县南屿镇南井村松杭洲</view>
    </view>
    <map></map>
  </view>
</template>

<script>
export default {

}
</script>

<style lang="scss">
  .contact{
    .img{
      width: 750rpx;
      height: 320rpx;
    }
    .info{
      view{
        padding: 10rpx 20rpx;
        line-height: 60rpx;
        border-bottom: 1px solid #eee
      }
    }
  }
</style>