<template>
	<view>
		<!-- 图片 -->
	<div>
	<uni-swiper-dot  :info="info" :current="current" field="content">
		<swiper class="swiper-box" @change="change">
			<swiper-item v-for="(item ,index) in info" :key="index">
				<view class="swiper-item">
					<image :src="item.url" style="width: 90%;" mode="scaleToFill"></image>
				</view>
			</swiper-item>
		</swiper>
	</uni-swiper-dot>
	</div>
		
		<!-- 介绍 -->
		<uni-card :is-shadow="false">
			<text>{{ticket.description}}</text>
		</uni-card>
		
<!-- 日期选择 -->
		<div style="width: 92%; margin: 0 auto;">
			<uni-datetime-picker type="date" :clear-icon="false" v-model="single" @maskClick="maskClick" />
		</div>
		

			<uni-card title="基础卡片" extra="额外信息" style="width: 90%;">
				<template v-slot:title>
					<div style="display: flex; justify-content: space-between;">
						<uni-list>
							<uni-list-item  title="游客信息"/>
						</uni-list>
						<uni-icons type="plusempty" size="25" style="margin: 10px;" @click="inputDialogToggle"></uni-icons>
					</div>

				</template>
				<view>
							<uni-table ref="table" :loading="loading" type="selection" stripe emptyText="暂无更多数据" @selection-change="selectionChange">
								<uni-tr>
									<uni-th align="center">姓名</uni-th>
									<uni-th align="center">号码</uni-th>
									<uni-th align="center" width="5">设置</uni-th>
								</uni-tr>
								<uni-tr v-for="(item, index) in tableData" :key="index">
									<uni-td align="center">
										<view class="name">{{ item.name }}</view>
									</uni-td>
									<uni-td align="center">{{ item.phone }}</uni-td>
									<uni-td align="center">
										<view class="uni-group">
											
											<uni-icons type="compose" size="25"></uni-icons>
											<uni-icons type="trash" size="25" color="red"></uni-icons>
<!-- 
											<button class="uni-button" size="mini" type="primary">修改</button> 
											<button class="uni-button" size="mini" type="warn">删除</button> -->
										</view>
									</uni-td>
								</uni-tr>
							</uni-table>
							<!-- <view class="uni-pagination-box"><uni-pagination show-icon :page-size="pageSize" :current="pageCurrent" :total="total" @change="change" /></view> -->
						</view>
			</uni-card>

	

	<!-- 购买 -->
		<uni-card style="width: 100%; margin: 0px; left: 0px; bottom: 0px;">
			<div style="display: flex; justify-content: space-between;">
				<text style="font-size: 18px; margin-top: 5px;">￥: 20</text>
				<button type="primary" size="mini" style="margin-right: 10%;">购买</button>
			</div>
		</uni-card>
				
	<!-- 新增用户 -->
		<uni-popup ref="inputDialog" type="dialog">
			<uni-popup-dialog ref="inputClose"  mode="input" title="新增游客" value="对话框预置提示内容!"
				placeholder="请输入内容" @confirm="dialogInputConfirm">
				<uni-section title="填写游客信息" type="line">
				
				<view class="example">
				<uni-forms ref="baseForm" :modelValue="baseFormData">
					<uni-forms-item label="姓名" required>
						<uni-easyinput v-model="baseFormData.name" placeholder="请输入姓名" />
					</uni-forms-item>
					<uni-forms-item label="身份证" required>
						<uni-easyinput v-model="baseFormData.age" placeholder="请输入身份证号" />
					</uni-forms-item>
					<uni-forms-item label="手机号" required>
						<uni-easyinput v-model="baseFormData.age" placeholder="请输入手机号" />
					</uni-forms-item>
					<uni-forms-item label="门票类型" required="">
						<uni-data-select v-model="userType" :localdata="ticketTypes" @change="change"></uni-data-select>
					</uni-forms-item>
				</uni-forms>
				</view>
			</uni-section>
			</uni-popup-dialog>
		</uni-popup>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				 array: ['中国', '美国', '巴西', '日本'],
				ticketTypes: [
					{value: 0, text: '成人票'},
					{value:1, text: '儿童票'},
					{value: 2, text: '学生票'}
					],
				baseFormData: {
					name: '',
					age: '',
					introduction: '',
					sex: 2,
					hobby: [5],
					datetimesingle: 1627529992399
				},
				ticket: {
					description: "岳麓山，因南北朝刘宋时《南岳记》“南岳sdfsfsdafgsfafdsadfsadfafsdaf周围八百里，回雁为首，岳麓为足”而得名。岳麓山位于湖南省长沙市岳麓区湘江西岸；橘子洲位于湘江中，由南至北，纵贯江心，西瞻岳麓，东临古城。岳麓山景区内现有植物174科559属977种，以典型的亚热带常绿阔叶林和亚..."
				},
				info: [{
				url: 'https://ns-strategy.cdn.bcebos.com/ns-strategy/upload/fc_big_pic/part-00484-2281.jpg',
			}, {
				url: 'https://ns-strategy.cdn.bcebos.com/ns-strategy/upload/fc_big_pic/part-00484-2281.jpg',
			}, {
				url: 'https://ns-strategy.cdn.bcebos.com/ns-strategy/upload/fc_big_pic/part-00484-2281.jpg',
			}],
			    userType: '',
				current: 0,
				searchVal: '',
				tableData: [{name: '张三', phone: 15055312615}],
				// 每页数据量
				pageSize: 10,
				// 当前页
				pageCurrent: 1,
				// 数据总量
				total: 0,
				loading: false,
				options: [{
					icon: 'chat',
					text: '客服'
				}, {
					icon: 'shop',
					text: '店铺',
					info: 2,
					infoBackgroundColor: '#007aff',
					infoColor: "#f5f5f5"
				}, {
					icon: 'cart',
					text: '购物车',
					info: 2
				}],
				customButtonGroup1: [{
					text: '立即购买',
					backgroundColor: 'linear-gradient(90deg, #FE6035, #EF1224)',
					color: '#fff'
				}]
			}
		},
		methods: {
			bindPickerChange: function(e) {
			    console.log('picker发送选择改变，携带值为', e.detail.value)
			    this.index = e.detail.value
			},
			change(e) {
			this.current = e.detail.current;
			},
			onClick(e) {
				uni.showToast({
					title: `点击${e.content.text}`,
					icon: 'none'
				})
			},
			buttonClick(e) {
				console.log(e)
				this.options[2].info++
			},
			inputDialogToggle() {
				this.$refs.inputDialog.open()
			},
		}
	}
</script>

<style>
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
