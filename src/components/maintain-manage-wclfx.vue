<template>
	<div class="maintain-manage-wclfx">
		<div class="additional-box">
	    <el-select size="small" v-model="month" placeholder="选择月" style="margin-right: 5px;">
		    <el-option
		      v-for="item in options"
		      :key="item.value"
		      :label="item.label"
		      :value="item.value">
		    </el-option>
		  </el-select>

	    <el-select size="small" v-model="business" placeholder="请选择">
		    <el-option
		      v-for="item in options"
		      :key="item.value"
		      :label="item.label"
		      :value="item.value">
		    </el-option>
		  </el-select>
  	</div>

  	<div class="tongji-box">
  		<div>
  			<el-progress color="#c78866" type="circle" :percentage="80" :stroke-width="12" :width="100" />
  			<p style="color: #c78866">作业覆盖率</p>
  		</div>

  		<div>
  			<el-progress color="#67c99c" type="circle" :percentage="80" :stroke-width="12" :width="100" />
  			<p style="color: #67c99c">计划完成率</p>
  		</div>

  		<div>
  			<el-progress color="#ea3323" type="circle" :percentage="80" :stroke-width="12" :width="100" />
  			<p style="color: #ea3323">问题整改率</p>
  		</div>

  		<div>
  			<el-progress color="#5e199a" type="circle" :percentage="80" :stroke-width="12" :width="100" />
  			<p style="color: #5e199a">督办件办结率</p>
  		</div>
  	</div>
	</div>
</template>


<script>
	export default {
		name: 'maintain-manage-wclfx',
		data() {
			return {
				month: '',
				options: [],
				business: ''
			}
		}
	}
</script>

<style lang="less" scoped>
@bgColor: rgba(0, 0, 0, 0.7);
@sysColor: #4aa3a4;

.maintain-manage-wclfx {
	color: @sysColor;
	.zyjhlss {
		display: flex;
		align-items: center;
		> span {
			margin-right: 20px;
			&:nth-of-type(1) {
				display: inline-block;
				width: 120px;
			}
		}
	}
	.monitor-value {
		font-size: 30px;
		color: #7dfb4c;
	}
}

.tongji-box {
	display: flex;
	justify-content: space-around;
	margin-top: 10px;
	> div {
		p {
			text-align: center;
			margin-top: 20px;
			font-size: 20px;
		}
	}
}

/deep/ .el-progress__text {
	color: #abf04b;
}

/deep/ .el-select{
	// background-color: red;
	.el-input__inner {
		background-color: rgba(74, 163, 164, .6);
		border-color: @sysColor;
		// border: none;
		width: 150px;
	}
}
	
</style>