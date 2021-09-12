<template>

	<div>
		<el-row :gutter="20">
		  <el-col :span="6"><div class="grid-content bg-purple">台账编号</div></el-col>
		  <el-col :span="6"><div class="grid-content bg-purple">台账名称</div></el-col>
		  <el-col :span="6"><div class="grid-content bg-purple">养护单位</div></el-col>
		  <el-col :span="6"><div class="grid-content bg-purple">面积</div></el-col>
		</el-row>


		<el-row 
			:gutter="20" 
			v-for="({ date, name, address, value }, index) in tableData" 
			:key="name" class="tableItem" @click.native="bindClick(tableData[index])">
		  <el-col :span="6"><div class="grid-content bg-purple">{{date}}</div></el-col>
		  <el-col :span="6"><div class="grid-content bg-purple">{{name}}</div></el-col>
		  <el-col :span="6"><div class="grid-content bg-purple">{{address}}</div></el-col>
		  <el-col :span="6"><div class="grid-content bg-purple">{{value}}</div></el-col>
		</el-row>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				tableData: [
					{ date: '1111', name: '222', address: 'eeee', value: '5555' },
					{ date: '1111', name: '222', address: 'eeee', value: '5555' },
				]
			}
		},
		methods: {
			bindClick(item) {
				this.$emit('click', item);
			}
		}
	}
</script>

<style lang="less" scoped>
	@bgColor: rgba(0, 0, 0, 0.7);
	@sysColor: #4aa3a4;

	/deep/ .grid-content.bg-purple {
		// text-align: left;
		padding-left: 10px;
		color: @sysColor;
	}
	.tableItem {
		.grid-content.bg-purple {
			// padding: 7px 0;
			line-height: 30px;
			cursor: pointer;
		}
	}
</style>



