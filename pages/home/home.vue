<template>
	<view class="page">
		<view class="header-bento">
			<view class="bento-grid">
				<view class="bento-item welcome-box">
					<text class="title">SecondHand</text>
					<text class="welcome-text">Hi, {{ username }}</text>
					<view class="status-tag">校园版</view>
				</view>
				<view class="bento-item search-box">
					<input class="search-input" placeholder="搜索商品..." />
				</view>
				<view class="bento-item mini-stats">
					<text class="stats-num">{{ goods.length }}</text>
					<text class="stats-label">在售</text>
				</view>
			</view>

			<scroll-view scroll-x="true" class="category-scroll">
				<view class="category-inner">
					<view v-for="(item, index) in categories" :key="index"
						:class="['category-pill', activeCategory === item ? 'active' : '']" 
						@click="activeCategory = item">
						{{ item }}
					</view>
				</view>
			</scroll-view>
		</view>

		<view class="waterfall-container">
			<view class="waterfall-column">
				<view v-for="(item, index) in leftList" :key="index" class="product-card">
					<image :src="item.img" mode="widthFix" class="product-img"></image>
					<view class="product-info">
						<text class="product-name">{{ item.title }}</text>
						<text class="product-price">￥{{ item.price }}</text>
					</view>
				</view>
			</view>
			<view class="waterfall-column">
				<view v-for="(item, index) in rightList" :key="index" class="product-card">
					<image :src="item.img" mode="widthFix" class="product-img"></image>
					<view class="product-info">
						<text class="product-name">{{ item.title }}</text>
						<text class="product-price">￥{{ item.price }}</text>
					</view>
				</view>
			</view>
		</view>

		<view class="tabbar-wrap">
			<view class="tabbar-glass">
				<view class="tab-item active">首页</view>
				<view class="tab-item">发现</view>
				<view class="add-btn">+</view>
				<view class="tab-item">消息</view>
				<view class="tab-item">我的</view>
			</view>
		</view>
	</view>
</template>

<script>
	// 注意：如果你用的是 uni-app x，这里不能写 setup 简写，改用传统 export 写法最稳
	export default {
		data() {
			return {
				username: 'roboo_user',
				activeCategory: '全部',
				categories: ['全部', '数码产品', '潮流穿搭', '二手书籍', '运动户外', '生活百货'],
				goods: [
					{ title: 'iPhone 13 降价急出', price: 3199, img: 'https://picsum.photos/300/400?r=1' },
					{ title: '极简白台灯', price: 45, img: 'https://picsum.photos/300/300?r=2' },
					{ title: '考研英语词汇书', price: 15, img: 'https://picsum.photos/300/500?r=3' },
					{ title: '机械键盘 99新', price: 199, img: 'https://picsum.photos/300/350?r=4' },
					{ title: '滑板入门级', price: 80, img: 'https://picsum.photos/300/450?r=5' },
					{ title: '潮流卫衣', price: 65, img: 'https://picsum.photos/300/320?r=6' }
				]
			}
		},
		computed: {
			leftList() {
				return this.goods.filter((_, i) => i % 2 === 0);
			},
			rightList() {
				return this.goods.filter((_, i) => i % 2 === 1);
			}
		}
	}
</script>

<style scoped lang="scss">
	.page {
		background: #f6f8ef;
		min-height: 100vh;
		padding: 30rpx;
		padding-bottom: 200rpx;
	}

	/* Bento Grid */
	.header-bento {
		margin-bottom: 30rpx;
		.bento-grid {
			display: grid;
			grid-template-columns: 1.6fr 1fr;
			gap: 20rpx;
			.bento-item {
				background: #fff;
				border-radius: 40rpx;
				padding: 30rpx;
				border: 1px solid rgba(0,0,0,0.05);
			}
			.welcome-box { 
				grid-row: span 2; 
				.title { font-size: 36rpx; font-weight: bold; color: #1a1a1a; display: block; }
				.welcome-text { font-size: 24rpx; color: #999; margin-top: 10rpx; }
				.status-tag { margin-top: 20rpx; background: #000; color: #fff; padding: 4rpx 16rpx; border-radius: 10rpx; font-size: 20rpx; width: fit-content; }
			}
			.search-box { display: flex; align-items: center; .search-input { font-size: 24rpx; width: 100%; } }
			.mini-stats { display: flex; flex-direction: column; align-items: center; .stats-num { font-size: 32rpx; font-weight: bold; color: #9edb72; } .stats-label { font-size: 20rpx; color: #ccc; } }
		}
	}

	/* 分类横向滚动修复 */
	.category-scroll {
		width: 100%;
		margin-top: 30rpx;
		white-space: nowrap;
		height: 80rpx;
	}
	.category-inner {
		display: flex;
		flex-direction: row;
		align-items: center;
	}
	.category-pill {
		display: inline-block;
		padding: 12rpx 35rpx;
		background: #fff;
		border-radius: 100rpx;
		margin-right: 15rpx;
		font-size: 24rpx;
		flex-shrink: 0;
		&.active { background: #d8ec57; font-weight: bold; border: 1px solid #c0d63d; }
	}

	/* 瀑布流布局修复 */
	.waterfall-container {
		display: flex;
		justify-content: space-between;
		gap: 20rpx;
		margin-top: 30rpx;
	}
	.waterfall-column {
		flex: 1;
		display: flex;
		flex-direction: column;
		gap: 20rpx;
	}
	.product-card {
		background: #fff;
		border-radius: 30rpx;
		overflow: hidden;
		box-shadow: 0 4rpx 15rpx rgba(0,0,0,0.03);
		.product-img { width: 100%; height: auto; display: block; }
		.product-info { padding: 20rpx; .product-name { font-size: 24rpx; color: #333; } .product-price { font-size: 32rpx; font-weight: bold; margin-top: 10rpx; display: block; } }
	}

	/* 底部 Tabbar */
	.tabbar-wrap {
		position: fixed;
		bottom: 40rpx; left: 40rpx; right: 40rpx;
		z-index: 100;
		.tabbar-glass {
			height: 110rpx; background: rgba(255,255,255,0.95); backdrop-filter: blur(10px);
			border-radius: 100rpx; display: flex; justify-content: space-around; align-items: center;
			box-shadow: 0 10rpx 40rpx rgba(0,0,0,0.1);
		}
		.tab-item { font-size: 24rpx; color: #ccc; &.active { color: #000; font-weight: bold; } }
		.add-btn { width: 90rpx; height: 90rpx; background: #000; color: #fff; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 40rpx; margin-top: -60rpx; border: 6rpx solid #f6f8ef; }
	}
</style>