<template>
  <div class="maintain-manage mapbox">
    <MMap ref="map"></MMap>
    <div class="top">
      <div class="top-left">
        <el-button class="ghost-button" size="small">养护管理系统</el-button>
        <el-button class="ghost-button" size="small" @click="isShowWclfx = true">养护作业完成率分析</el-button>
        <el-button class="ghost-button" size="small" @click="isShowMonitoring = true">养护作业监督情况</el-button>
        <el-button class="ghost-button" size="small" @click="isShowYhldfx = true">养护单位养护绿地分析</el-button>
      </div>
      <p>{{currentTime}}</p>
      <!-- 地图图层配置 -->
      <div class="top-right">
        <span v-for="({ label, key, funcName }) in layerConfig" :key="key" :class="{ active: activeMapLayer === key }" @click="layerConfigBindClick(key, funcName)">
          {{label}}
        </span>
      </div>
    </div>
    <div class="overview">
      <div class="situation">
        <p class="title">
          <img src="../assets/icon_maintain_01.png" class="icon-maintain" alt="">
          <span>2021年绿地养护总体情况</span>
        </p>
        <div class="situation-content">
          <p class="tac" style="line-height: 30px;">中心管理绿地养护总面积</p>
          <p class="tac value-s" style="font-size: 25px;">43443</p>
          <div class="level-statistics">
            <div>
              <p><span>⭐️⭐️⭐️</span>特级</p>
              <p class="value-s">30</p>
            </div>
            <div>
              <p><span>⭐️⭐️</span>一级</p>
              <p class="value-s">30</p>
            </div>
            <div>
              <p><span>⭐️</span>二级</p>
              <p class="value-s">30</p>
            </div>
          </div>
        </div>
      </div>
      <div class="maintenance-work">
        <p class="title">
          <span>全区本月养护工作</span>
        </p>
        <div class="echarts-box">
          <div class="coverage-box">
            <!-- <div class="coverage"></div> -->
            <el-progress color="#8bc4e3" type="circle" :percentage="80" :stroke-width="12" :width="100" />
            <p class="desc">问题覆盖率</p>
          </div>
          <div class="rectification-box">
            <!-- <div class="rectification"></div> -->
            <el-progress color="#ea3323" type="circle" :percentage="80" :stroke-width="12" :width="100" />
            <p class="desc">问题整改率</p>
          </div>
        </div>
      </div>
      <div class="realtime">
        <p class="title">
          <img src="../assets/icon_maintain_01.png" class="icon-maintain" alt="">
          <span>2021年09月10日养护情况</span>
        </p>
        <div class="realtime-content">
          <div style="padding-left: 15px;">
            <p class="image-text-box">
              <img src="../assets/icon_maintain_user.png" class="icon-maintain" alt="">
              <span>今日养护人员</span>
            </p>
            <span class="realtime-content-value" style="margin-left: 40px">2000</span>
          </div>

          <div style="display: flex;justify-content: space-around;margin-top: 7px;">
          	<div>
	            <p class="image-text-box">
	              <img src="../assets/icon_maintain_user.png" class="icon-maintain" alt="">
	              <span>巡查问题</span>
	            </p>
	            <span class="realtime-content-value"  style="margin-left: 40px">20</span>
	          </div>

	          <div>
	          	<p>已处理</p>
	          	<p class="realtime-content-value tac">2件</p>
	          </div>

	          <div>
	          	<p>未处理</p>
	          	<p class="realtime-content-value-non tac">20</p>
	          </div>
          </div>

          <div style="display: flex;justify-content: space-around;margin-top: 7px;">
          	<div>
	            <p class="image-text-box">
	              <img src="../assets/icon_maintain_user.png" class="icon-maintain" alt="">
	              <span>督办案件</span>
	            </p>
	            <span class="realtime-content-value" style="margin-left: 40px">20</span>
	          </div>

	          <div>
	          	<p>已处理</p>
	          	<p class="realtime-content-value tac">2件</p>
	          </div>

	          <div>
	          	<p>未处理</p>
	          	<p class="realtime-content-value-non tac">20</p>
	          </div>
          </div>
        </div>
      </div>
    </div>

    <div class="search-box">
    	<el-input
    		ref="searchInput"
    		@keydown.enter.native="isShowResult = true"
		    placeholder="" 
		    suffix-icon="el-icon-search"
		    v-model="input1">
		  </el-input>

		  <el-button style="margin-left: 10px;">全区本月养护工作覆盖面分析</el-button>
		  <el-button>全区本月养护工作聚集分析</el-button>
    </div>
    <div class="map-layers">
    	<el-collapse v-model="activeNames">
			  <el-collapse-item name="1">
			  	<template slot="title">
			      <div class="layer-image-text-box">
			      	<img src="../assets/layers.png" class="icon-maintain" alt="">
			      	<span>图层</span>
			      </div>
			    </template>

			    <div v-for="item in layersData" :key="item.label" class="layer-item">
			    	<p class="layer-image-text-box">
			    		<img :src="item.img" alt="">
			    		<span>{{item.label}}</span>
			    	</p>
			    	<el-switch v-model="item.checked"></el-switch>
			    </div>
			  </el-collapse-item>
			</el-collapse>
    </div>

    <el-dialog title="查询结果" :visible.sync="isShowResult">
    	<maintain-manage-result />
    </el-dialog>

    <el-dialog title="养护作业监督情况" :visible.sync="isShowMonitoring">
    	<maintain-manage-monitoring />
    </el-dialog>

    <el-dialog title="各项养护作业完成率分析" :visible.sync="isShowWclfx">
    	<maintain-manage-wclfx />
    </el-dialog>

    <el-dialog title="养护单位养护绿地分析" :visible.sync="isShowYhldfx">
    	<maintain-manage-yhldfx />
    </el-dialog>

    <el-dialog title="养护绿地信息" :visible.sync="isShowYhldxx" width="500px">
    	<maintain-manage-yhldxx />
    </el-dialog>

  </div>
</template>

<script>
	import MMap from './m-map.vue'
	import moment from 'moment'
	import * as echarts from 'echarts'
	import { returnRateOptions } from './echarts-func.js'
	import imageA from '../assets/imageA.png'
	import imageB from '../assets/imageB.png'
	import imageC from '../assets/imageC.png'

	/* 查询结果 */
	import MaintainManageResult from './maintain-manage-result.vue'
	/* 养护作业监督情况 */
	import MaintainManageMonitoring from './maintain-manage-monitoring.vue'
	/* 各养护作业完成率分析 */
	import MaintainManageWclfx from './maintain-manage-wclfx.vue'
	/* 养护单位养护绿地分析 */
	import MaintainManageYhldfx from './maintain-manage-yhldfx.vue'
	/* 养护绿地信息 */
	import MaintainManageYhldxx from './maintain-manage-yhldxx.vue'

	const layerConfig = [
		{ label: '2d地图', key: '2d', funcName: 'setMapLayer2d' },
		{ label: '卫星地图', key: 'satellite', funcName: 'setMapLayerSatellite' }
	]

	export default {
		components: {
			MMap,
			MaintainManageResult,
			MaintainManageMonitoring,
			MaintainManageWclfx,
			MaintainManageYhldfx,
			MaintainManageYhldxx
		},
		data() {
			return {
				currentTime: moment().format('YYYY年MM月DD日'),
				activeMapLayer: '2d',
				layerConfig,
				layersData: [
					{ label: '养护绿地', img: imageA, checked: true },
					{ label: '实时养护人员', img: imageB, checked: false },
					{ label: '待整改问题', img: imageC, checked: false },
				],
				activeNames: '1',
				input1: '',

				/* 弹窗 */
				isShowResult: false,
				isShowMonitoring: false,
				isShowWclfx: false,
				isShowYhldfx: false,
				isShowYhldxx: false
			}
		},
		mounted() {
			// this.coverageEchart = echarts.init(document.querySelector('.coverage'));
			// this.rectificationEchart = echarts.init(document.querySelector('.rectification'));

			// this.coverageEchart.setOption(returnRateOptions({ color: '#8bc4e3', textColor: '#abf04b', value: 30 }))
			// this.rectificationEchart.setOption(returnRateOptions({ color: '#ea3323', textColor: '#abf04b', value: 40 }))

			// document.querySelector('.')
			this.$refs.searchInput.$el.querySelector('.el-input__suffix').onclick = function() {
				this.isShowResult = true;
			}
			this.$once('hook:beforeDestroy', () => {
				this.$refs.searchInput.$el.querySelector('.el-input__suffix').onclick = null;
			})
		},
		methods: {
			layerConfigBindClick(key, funcName) {
				this.activeMapLayer = key;
				this.$refs.map && this.$refs.map[funcName]();
			}
		}
	}
</script>

<style lang="less" scoped>
@bgColor: rgba(0, 0, 0, 0.7);
@sysColor: #4aa3a4;

.mapbox {
	position: relative;
	width: 100%;
	height: 100vh;
	color: @sysColor;
}

.top {
	position: absolute;
	top: 0;
	display: flex;
	justify-content: space-between;
	align-items: center;
	height: 50px;
	padding: 0 20px;
	width: 100%;
	box-sizing: border-box;
	color: @sysColor;
	background-color: @bgColor;
	.top-left {
		flex: 1;
	}
	.top-right {
		display: flex;
		justify-content: flex-end;
		flex: 1;
		font-size: 13px;
		color: white;
		> span {
			cursor: pointer;
			&.active {
				color: @sysColor;
			}
			&:nth-of-type(2) {
				margin-left: 7px;
			}
		}
	}
}

.maintain-manage {
	.map-layers {
		position: absolute;
		top: 50px;
		right: 0px;
		// height: 300px;
		width: 200px;
		box-sizing: border-box;
		// background-color: @bgColor;
		border-top: 4px solid @sysColor;
		.layer-image-text-box {
			display: flex;
			align-items: center;
			padding-left: 10px;
		}
		.layer-item {
			display: flex;
			justify-content: space-between;
			padding: 5px 10px;
			color: @sysColor;
			img {
				width: 20px;
				height: 20px;
				margin-right: 5px;
			}
			.layer-image-text-box {
				padding-left: 0px;
			}
		}
	}

	.search-box {
		display: flex;
		position: absolute;
		top: 60px;
		left: 310px;
		.el-input__suffix {
			cursor: pointer;
		}
	}
}

.overview {
	width: 300px;
	background-color: @bgColor;
	height: calc(100% - 50px);
	box-sizing: border-box;
	position: absolute;
	top: 50px;
	left: 0px;
	border-top: 4px solid @sysColor; 
	font-size: 13px;
	overflow: scroll;
	.title {
		display: flex;
		align-items: center;
		padding: 10px;
		border-bottom: 1.5px solid #e89f42;
		font-size: 14px;
	}
	.situation {
		.situation-content {
			.level-statistics {
				display: flex;
				justify-content: space-around;
				div {
					display: flex;
					flex-direction: column;
					align-items: center;
					p {
						&:nth-of-type(2) {
							font-size: 23px;
						}
					}
				}
			}
		}

		.value-s {
			color: #7dfb4c;
		}
	}

	.maintenance-work {
		margin-top: 30px;
		.echarts-box {
			display: flex;
			justify-content: space-around;
			> div {
				padding: 30px 10px 0px;
				.el-progress.el-progress--circle {
					margin-bottom: 10px;
				}
			}
			.rectification, .coverage {
				width: 150px;
				height: 150px;
			}
			.desc {
				text-align: center;
				font-size: 16px;
			}
		}
	}

	.realtime {
		margin-top: 30px;
		.image-text-box {
			display: flex;
			align-items: center;
		}
		.realtime-content {
			padding: 15px 0px;
			.realtime-content-value {
				// text
				color: #abf04b;
			}
			.realtime-content-value-non {
				color: red;
			}
		}
	}
}

.icon-maintain {
	width: 20px;
	height: 20px;
	margin-right: 10px;
}
.tac {
	text-align: center;
}
.ghost-button {
}

/deep/ .el-dialog {
  background-color: rgba(0,0,0,.7);
  position: relative;
  .el-dialog__header {
  	border-top: 2px solid @sysColor;
    border-bottom: 1px solid #e89f42;
    padding: 10px 20px;

    .el-dialog__title {
      color: @sysColor;
      font-size: 14px;
    }

    .el-dialog__headerbtn {
      top: 10px;
    }

    .el-dialog__close {
      font-size: 24px;
    }
  }

  .el-dialog__body {
  	min-height: 200px;
  }

  .additional-box {
		position: absolute;
		right: 60px;
		top: 7px;
	}
}
</style>

<style lang="less">
@bgColor: rgba(0, 0, 0, 0.7);
@sysColor: #4aa3a4;

.maintain-manage {
	.el-collapse {
		border-top: none;
		border-bottom: none;
		background-color: @bgColor;
	}
	.ghost-button {
		background-color: rgba(74, 163, 164, 0.3) !important;
		border-color: rgba(74, 163, 164, 0.8) !important;
		color: @sysColor !important;
		border-width: 1.5px;
	}
	.el-collapse-item__header {
		background-color: transparent;
		color: @sysColor;
		border-bottom: none;
	}
	.el-collapse-item__wrap {
		border-top: 1.5px solid #e89f42;
		background-color: transparent;
		border-bottom: none;
	}
	.el-switch.is-checked .el-switch__core {
		background-color: @sysColor;
	}
	.el-collapse-item__content {
		padding-top: 5px;
		padding-bottom: 10px;
	}
	.search-box {
		.el-input {
			.el-input__icon.el-icon-search {
				color: black;
			}
			.el-input__suffix {
				cursor: pointer;
			}
		}
		.el-button {
			background-color: #e89f42;
			color: white;
			border: none;
		}
		.el-input__inner {
			background-color: rgba(74, 163, 164, 0.6);
			border-color: rgba(74, 163, 164, 0.8);
			border-width: 2px;
			color: white;
			&:focus {
				border-color: rgba(74, 163, 164, 1);
				border-width: 2px;
			}
			&::placeholder {
				color: rgba(255, 255, 255, 0.5);
			}
		}
	}

	.el-progress__text {
		font-size: 25px !important;
	} 
}
</style>

<style lang="less">
	.maintain-manage {
		.coverage-box {
			.el-progress__text {
				color: #abf04b;
			}
		}
		.rectification-box {
			.el-progress__text {
				color: #abf04b;
			}
		}
	}

</style>








