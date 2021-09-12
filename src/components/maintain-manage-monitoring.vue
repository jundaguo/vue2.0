<template>
	<div class="maintain-manage-monitoring">
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

  	<div>
  		<p class="zyjhlss">
  			<span>重点监督内容：</span>
  			<span class="monitor-value">浇水 修建</span>
  		</p>

  		<p class="zyjhlss" style="margin: 15px 0;">
  			<span>监督点位：</span>
  			<span class="monitor-value">200个</span>
  		</p>

  		<div class="zyjhlss">
  			<span>作业计划落实率</span>
  			<el-progress color="#e89f42" type="circle" :percentage="80" :stroke-width="12" :width="100" />
  		</div>
  	</div>
	</div>
</template>


<script>
	export default {
		name: 'maintain-manage-monitoring',
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

.maintain-manage-monitoring {
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

/deep/ .el-progress__text {
	color: #e89f42;
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