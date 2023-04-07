<template>
	<view class="container">
		<!-- 轮播图 -->
	<uni-swiper-dot class="uni-swiper-dot-box" :info="info" :current="current" field="content">
		<swiper class="swiper-box" @change="change">
			<swiper-item v-for="(item ,index) in info" :key="index">
				<view class="swiper-item">
					<image :src="item.url" mode="scaleToFill"></image>
				</view>
			</swiper-item>
		</swiper>
	</uni-swiper-dot>
	
	<!-- 门票列表 -->
	<div>
		<h2 style="text-align: center; margin-top: 20px;">门票列表</h2>
		
		<div style="margin-top: 20px;">
			<uni-list>
				
				<uni-list-item clickable="true" @click="clickTicket" title="岳麓山" note="岳麓山是位于湖南长沙,非常美丽" showArrow>
					<template v-slot:header>
						<view class="slot-box">
							<image class="slot-image" src="https://img1.baidu.com/it/u=3645682753,2838782129&fm=253&fmt=auto&app=138&f=JPEG?w=751&h=500" mode="widthFix"></image>
						</view>
					</template>
				</uni-list-item>
			</uni-list>
		</div>
	</div>
	</view>
</template>

<script>
	export default {
		data() {
			return {
	
				info: [{
				url: 'https://ns-strategy.cdn.bcebos.com/ns-strategy/upload/fc_big_pic/part-00484-2281.jpg',
			}, {
				url: 'https://ns-strategy.cdn.bcebos.com/ns-strategy/upload/fc_big_pic/part-00484-2281.jpg',
			}, {
				url: 'https://ns-strategy.cdn.bcebos.com/ns-strategy/upload/fc_big_pic/part-00484-2281.jpg',
			}],
			current: 0,
			}
		},
		methods: {
			change(e) {
			this.current = e.detail.current;
			},
			clickTicket() {
				console.log("点击了门票123");
				uni.navigateTo({
					url: '/pages/ticketDetail/ticketDetail'
				})
			}
		}
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
	.slot-image {
			/* #ifndef APP-NVUE */
			display: block;
			/* #endif */
			margin-right: 10px;
			width: 100px;
			height: 100px;
		}
		
	.swiper-box {
		height: 200px;
	}
	

	.swiper-item {
		/* #ifndef APP-NVUE */
		display: flex;
		/* #endif */
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 200px;
		color: #fff;
	}
	
</style>
