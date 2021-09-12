<template>
	<div class="maintain-manage-yhldfx">
  	<div class="tongji-box">
  			<div class="echart-box"></div>
  	</div>
	</div>
</template>


<script>
	import * as Echarts from 'echarts'

	export default {
		name: 'maintain-manage-yhldfx',
		data() {
			return {
				month: '',
				options: [],
				business: '',
				option: {
				  backgroundColor: 'transparent',
				  grid: {
				  	top: 15
				  },
				  xAxis: {
				    type: 'category',
				    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
				  },
				  yAxis: {
				    type: 'value',
				    splitLine: {
					    lineStyle: {
				        // 使用深浅的间隔色
				        color: '#eceaea21'
					    }
						}
				  },
				  series: [{
				  	top: 0,
				    data: [120, 200, 150, 80, 70, 110, 130],
				    type: 'bar',
				    itemStyle: {
				      color: {
				        type: 'linear',
				        x: 0,
				        y: 0,
				        x2: 0,
				        y2: 1,
				        colorStops: [{
				          offset: 0,
				          color: '#83b6f0' // 0% 处的颜色
				        }, {
				          offset: 1,
				          color: '#428be9' // 100% 处的颜色
				        }],
				        global: false // 缺省为 false
				      }
				    }
				  }]
				}
			}
		},
		mounted() {
			this.chart1 = Echarts.init(document.querySelector('.echart-box'));
			this.chart1.setOption(this.option)
		}
	}
</script>

<style lang="less" scoped>
@bgColor: rgba(0, 0, 0, 0.7);
@sysColor: #4aa3a4;

.maintain-manage-yhldfx {
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

.echart-box {
	width: 100%;
	height: 300px;
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