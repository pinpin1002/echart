<template>
	<div class="container">
		<v-chart class="chart" :option="option" autoresize />
	</div>
</template>

<script setup>
import moment from "moment";
import { use } from "echarts/core";
import { CanvasRenderer } from "echarts/renderers";
import { PieChart, LineChart, BarChart, HeatmapChart } from "echarts/charts";
import {
	TitleComponent,
	TooltipComponent,
	LegendComponent,
	GridComponent,
	ToolboxComponent,
	VisualMapComponent,
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
	VisualMapComponent,
	HeatmapChart,
]);
let i = 0;
const option = ref({
	legend: {
		data: [
			"Viewership Previous(11/14~11/18)",
			"Viewership Current(11/14~11/18)",
			"Passerby Previous(11/14~11/18)",
			"Passerby Current(11/14~11/18)",
		],
		formatter: (value) => {
			let prefixTitle = i % 2 === 0 ? value.split(" ")[0] : "";

			const suffixTitle = value.split(" ")[1];

			i++;
			return `${prefixTitle} {label|} {spacer1|${suffixTitle}}`;
		},
		textStyle: {
			rich: {
				label: {
					width: 20,
					height: 8,
					backgroundColor: "red",
					padding: 0,
					borderWidth: 1,
					verticalAlign: "center",
					// borderColor: "black",
					// borderType: "dashed",
				},
				spacer1: {
					padding: 0,
					// width: 50,
					verticalAlign: "center",
					align: "center",
				},
			},
		},

		icon: "none",
	},
	color: ["#b7daff", "#0062cc", "#d682ff", "#6e328b"],
	grid: { bottom: "center", left: "center", width: "90%", height: "60%" },
	tooltip: {
		trigger: "axis",
		axisPointer: {
			type: "cross",
			crossStyle: {
				color: "#999",
			},
		},
	},
	xAxis: [
		{
			type: "category",
			axisTick: { alignWithLabel: true },
			data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
			axisPointer: {
				type: "none",
			},
		},
	],
	yAxis: [
		{
			type: "value",
			name: "Times",
			min: 0,
			max: 4000,
			interval: 1000,
			splitLine: {
				show: false,
			},
			axisLine: {
				show: true,
				lineStyle: {
					color: "#000",
				},
			},
		},
		{
			type: "value",
			name: "Visitors",
			min: 0,
			max: 50000,
			interval: 10000,
			splitLine: {
				show: false,
			},
			axisLine: {
				show: true,
				lineStyle: {
					color: "#000",
				},
			},
		},
	],
	series: [
		{
			name: "Viewership Previous(11/14~11/18)",
			type: "bar",
			barGap: 0,
			barCategoryGap: 100,
			tooltip: {
				valueFormatter: function (value) {
					return value + " 次";
				},
			},
			data: [
				2000, 3900, 700, 2320, 2560, 767, 1356, 1622, 3260, 2000, 3604, 3300,
			],
		},
		{
			name: "Viewership Current(11/14~11/18)",
			type: "bar",
			barGap: 0,
			barCategoryGap: 100,
			tooltip: {
				valueFormatter: function (value) {
					return value + " 人";
				},
			},
			data: [
				2600, 2900, 2000, 2604, 2870, 3007, 1706, 1202, 2007, 1808, 6000, 2003,
			],
		},
		{
			name: "Passerby Previous(11/14~11/18)",
			type: "line",
			symbol: "circle",
			symbolSize: 6,
			lineStyle: { type: "dashed" },
			yAxisIndex: 1,
			tooltip: {
				valueFormatter: function (value) {
					return value + "次";
				},
			},
			data: [
				20000, 40000, 45000, 40000, 10000, 35000, 20000, 23000, 23000, 16000,
				12000, 40000,
			],
		},
		{
			name: "Passerby Current(11/14~11/18)",
			type: "line",
			symbol: "circle",
			symbolSize: 6,
			lineStyle: { type: "dashed" },
			yAxisIndex: 1,
			tooltip: {
				valueFormatter: function (value) {
					return value + "人";
				},
			},
			data: [
				20000, 22000, 33000, 45000, 43000, 10020, 20300, 23400, 23000, 16050,
				12000, 60200,
			],
		},
	],
});
</script>

<style scoped>
.container {
	height: 500px;
}
</style>
