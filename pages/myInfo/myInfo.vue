<template>	
	<view class="uni-container">
		<uni-card>
			<uni-list-chat title="King" :avatar-list="avatarList" note="手机号: 15055312715" time="2020-02-02 20:20" badge-positon="left" badge-text="dot">
			<view class="chat-custom-right" style="margin-top: 50%;">
				<!-- 需要使用 uni-icons 请自行引入 -->
				<uni-icons type="forward" color="#999" size="20"></uni-icons>
			</view>
			</uni-list-chat>
		</uni-card>
		<uni-card title="我的订单记录">
			
			<uni-table ref="table" :loading="loading"  stripe emptyText="暂无更多数据" @selection-change="selectionChange">
				<uni-tr>
					<uni-th  align="center" width="2">日期</uni-th>
					<uni-th  align="center" width="5">门票</uni-th>
					<uni-th align="center" width="2">人数</uni-th>
					<uni-th align="center" width="5">设置</uni-th>
				</uni-tr>
				<uni-tr v-for="(item, index) in tableData" :key="index">
					<uni-td align="center">{{ item.date }}</uni-td>
					<uni-td align="center">
						<view class="name">{{ item.name }}</view>
					</uni-td>
					<uni-td align="center">{{ item.number }}</uni-td>
					<uni-td align="center">
					
							<button class="uni-button" size="mini" type="primary">详情</button>
							<button class="uni-button" size="mini" type="warn">删除</button>
	
					</uni-td>
				</uni-tr>
			</uni-table>
			<view class="uni-pagination-box"><uni-pagination show-icon :page-size="pageSize" :current="pageCurrent" :total="total" @change="change" /></view>
		</uni-card>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			searchVal: '',
			tableData: [{date: '2023-03.12', name: '岳麓山', number: 2, text: '测试'}],
			// 每页数据量
			pageSize: 10,
			// 当前页
			pageCurrent: 1,
			// 数据总量
			total: 0,
			loading: false,
			avatarList: [{
							url: 'https://web-assets.dcloud.net.cn/unidoc/zh/unicloudlogo.png'
						}],
			}
		},
		onLoad() {
		this.selectedIndexs = []
		this.getData(1)
	},
		methods: {
			
		}
	}
</script>

<style>
.uni-group {
	display: flex;
	align-items: center;
}
</style>
