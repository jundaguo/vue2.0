<template>
	<div class="maintain-manage-yhldxx">
		<p>
			<span>台账编号：</span>
			<span>123</span>
		</p>

		<p>
			<span>绿地名称：</span>
			<span>123</span>
		</p>

		<p>
			<span>类型：</span>
			<span>123</span>
		</p>

		<p>
			<span>面积：</span>
			<span>123</span>
		</p>

		<p>
			<span>养护公司：</span>
			<span>123</span>
		</p>
	</div>
</template>


<script>
	export default {

	}
</script>

<style lang="less" scoped>
@bgColor: rgba(0, 0, 0, 0.7);
@sysColor: #4aa3a4;

	.maintain-manage-yhldxx {
		color: @sysColor;
		p {
			line-height: 35px;
			span {
				&:nth-of-type(1) {
					display: inline-block;
					// width: 70px;
				}
			}
		}
	}
</style>