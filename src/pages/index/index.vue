<template>
	<view class="home">
		<!-- 轮播图 -->
		<swiper indicator-dots autoplay circular>
			<swiper-item v-for="item in swipers" :key="item.id">
				<image :src="item.img" mode="scaleToFill" />
			</swiper-item>
		</swiper>
		<!-- 导航区域 -->
		<view class="nav">
			<view class="nav_item" v-for="item in navs" :key="item.id" @click="navItemClick(item.path)">
				<view :class="item.icon"></view>
				<text>{{ item.title }}</text>
			</view>
		</view>
		<!-- 推荐商品 -->
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<view class="goods_list">
				<view class="goods_item" v-for="item in hotgoods" :key="item.goods_id">
					<image :src="item.img_url" mode="scaleToFill" />
					<view class="price">
						<text>{{item.sell_price}}</text>
						<text class="name">{{ item.market_price }}</text>
					</view>
					<view>
						<text>{{item.title}}</text>
					</view>
				</view>
			</view>
			<GoodList :hotgoods="hotgoods"/>
		</view>
	</view>
</template>

<script>
import { loader } from '@dcloudio/uni-cli-shared/lib/url-loader';
import GoodList from "../../components/goodList/GoodList"
export default {
	components:{GoodList},
	data() {
		return {
			swipers: [],
			hotgoods: [],
			navs: [
				{
					id: 1,
					icon: "iconfont icon-ziyuan",
					title: "小陈超市",
					path: "/pages/goods/goods"
				},
				{
					id: 2,
					icon: "iconfont icon-guanyuwomen",
					title: "联系我们",
					path: "/pages/contact/contact"
				},
				{
					id: 3,
					icon: "iconfont icon-tupian",
					title: "社区图片",
					path: "/pages/news/news"
				},
				{
					id: 4,
					icon: "iconfont icon-shipin",
					title: "学习视频",
					path: "/pages/contact/contact"
				},
			]
		};
	},
	onLoad() {
		this.getSwipers(),
			this.getHotGoods();
	},
	methods: {
		// 获取轮播图的数据
		async getSwipers() {
			// uni.request({
			// 	url:'https://api-hmugo-web.itheima.net/api/public/v1/home/swiperdata',
			// 	success:res=>{
			// 		this.swipers = res.data.message
			// 	}
			// })
			const res = await this.$myRequest({
				url: "/api/getlunbo"
			});
			this.swipers = res.data.message;
			console.log(res);
		},

		async getHotGoods() {
			const res = await this.$myRequest({
				url: "/api/getgoods?pageindex=1"
			});
			this.hotgoods = res.data.message;
		},
		// 导航点击的数据处理函数
		navItemClick(url) {
			uni.navigateTo({
				url: url
			});
		}
	},
}
</script>
<style lang="scss"  scoped>
.home {
	swiper {
		width: 750rpx;
		height: 380rpx;

		image {
			height: 100%;
			width: 100%;
		}
	}

	.nav {
		display: flex;

		.nav_item {
			width: 25%;
			text-align: center;

			view {
				width: 120rpx;
				height: 120rpx;
				background-color: $uni-shop-color;
				border-radius: 60rpx;
				margin: 10px auto;
				line-height: 120rpx;
				color: white;
				font-size: 50rpx
			}

			text {
				font-size: 30rpx;
			}
		}
	}

	.hot_goods {
		background-color: #eee;
		overflow: hidden;
		margin-top: 10px;

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
		.tit {
			height: 50px;
			line-height: 50px;
			color: $uni-shop-color;
			text-align: center;
			letter-spacing: 20rpx;
			background-color: #fff;
			margin: 7rpx 0;
		}

	}
}
</style>
