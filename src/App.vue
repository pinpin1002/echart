<template>
	<div class="wrap">
		<div class="item-a">
			<v-chart class="chart" :option="option" autoresize />
		</div>
		<div class="item-b">2</div>
		<div class="item-c">3</div>
		<div class="item-d"></div>
	</div>
</template>

<script setup>
import moment from "moment";
import { use } from "echarts/core";
import { CanvasRenderer } from "echarts/renderers";
import { PieChart, LineChart, BarChart } from "echarts/charts";
import {
	TitleComponent,
	TooltipComponent,
	LegendComponent,
	GridComponent,
	ToolboxComponent,
} from "echarts/components";
import VChart from "vue-echarts";
import { ref } from "vue";

use([
	CanvasRenderer,
	PieChart,
	TitleComponent,
	TooltipComponent,
	LegendComponent,
	LineChart,
	GridComponent,
	ToolboxComponent,
	BarChart,
]);
const colors = ["rgba(46,147,250,0.7)"];
const datas = [
	["2024-10-1", 450],
	["2024-10-2", 550],
	["2024-10-3", 590],
	["2024-10-4", 580],
	["2024-10-5", 540],
	["2024-10-6", 500],
	["2024-10-7", 600],
	["2024-10-8", 530],
	["2024-10-9", 530],
	["2024-10-10", 580],
	["2024-10-11", 540],
	["2024-10-12", 455],
	["2024-10-13", 555],
];
const option = ref({
	color: colors,
	tooltip: {
		trigger: "axis",
		axisPointer: {
			type: "cross",
		},
	},
	grid: {
		bottom: "40%",
	},

	xAxis: [
		{
			type: "category",
			boundaryGap: false,
			axisTick: { show: true, length: 20 },
			axisLabel: {
				formatter: (value) => {
					return moment(value).format("yyyy/MM");
				},
				interval: datas.length - 2, // x軸間隔 如果只顯示頭尾兩端 則data長度減掉2
				margin: 30,
			},
			axisLine: {
				show: false,
				lineStyle: {
					color: "#ccc",
				},
			},
		},
	],
	yAxis: [
		{
			type: "value",
			position: "left",
			alignTicks: true,
			axisLabel: {
				show: false,
			},
			splitLine: { show: false },
			axisLine: {
				show: true,
				lineStyle: {
					color: "#ccc",
				},
			},
		},
		{
			type: "value",
			position: "right",
			alignTicks: true,
			splitLine: { show: false },
			axisLine: {
				show: true,
				lineStyle: {
					color: "#ccc",
				},
			},
		},
	],
	series: [
		{
			name: "View Count",
			type: "line",
			showSymbol: false,
			smooth: true,
			areaStyle: {},
			data: datas,
		},
	],
});
</script>

<style scoped>
.wrap {
	display: grid;
	grid-template-columns: 300px 50px auto 50px 200px;
	grid-template-rows: 25% 100px auto;
	grid-template-areas:
		"header main main main main"
		"side  main main main main"
		"side footer footer footer footer";
	height: 100vh;
	margin: 0 auto;
}
.item-a {
	grid-area: header;
	background-color: purple;
}
.item-b {
	grid-area: main;
	background-color: orange;
}
.item-c {
	grid-area: side;
	background-color: green;
}
.item-d {
	grid-area: footer;
	background-color: gray;
}
</style>
