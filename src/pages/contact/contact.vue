<template>
  <view class="contact">
    <image class="img" src="https://raw.githubusercontent.com/c2wzz/CCW_SHOP/master/src/static/aboutUs.png"
      mode="scaleToFill" />
    <view class="info">
      <view @click="callMe">联系电话:400-8828-8820 (点击拨打)</view>
      <view>联系地址:福建省福州市闽侯县旗山万佛寺天王殿</view>
    </view>
    <map class="map" :longitude="longitude" :latitude="latitude" :markers="WanfoTemple"></map>
  </view>
</template>

<script>
export default {
  data() {
    return {
      longitude: 119.212869,
      latitude: 25.99064,
      WanfoTemple: [
        {
          longitude: 119.212869,
          latitude: 25.99064,
          iconPath: '../../static/hmlogo.png',
          width:50,
          height:50
        }
      ]
    }
  },
  methods:{
    callMe(){
      uni.makePhoneCall({
        phoneNumber:'18649834737'
      })
    }
  }

}
</script>

<style lang="scss">
.contact {
  .img {
    width: 750rpx;
    height: 320rpx;
  }

  .info {
    view {
      padding: 10rpx 20rpx;
      line-height: 60rpx;
      border-bottom: 1px solid #eee
    }
  }

  .map {
    width: 750rpx;
    height: 750rpx;
  }
}
</style>