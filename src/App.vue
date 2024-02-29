<template>
	<!-- <div class="wrap">
		<div class="item-a">
			<v-chart class="chart" :option="option" autoresize />
		</div>
		<div class="item-b">
			
		</div>
		<div class="item-c">3</div>
		<div class="item-d"></div>
	</div> -->

	<div class="container">
		<!-- <v-chart class="chart" :option="heatMapoption" autoresize /> -->
		<v-chart class="chart" :option="maleOption" autoresize />
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
// heatmap
const hours = ["12a", "1a", "2a", "3a", "4a", "5a", "6a", "7a"];
// prettier-ignore
const days = [
    'Mon', 'Tue', 'Wed','Thr', 'Fri', 'Sat', 'Sun'
];
// prettier-ignore
//用2維表示 item[0] 為x軸 item[1] 為y軸 item[2] 為value
const data = [[0, 0, 100], [0, 1, 221], [0, 2, 232], [0, 3, 345], [0, 4, 258], [0, 5, 162], [0, 6, 473],[0, 7, 43],[1, 0, 283], [1, 1, 921], [1, 2, 112], [1, 3, 1101], [1, 4, 120], [1, 5, 1203], [1, 6, 1340], [1, 7, 3125],[2, 0, 4126], [2, 1, 121], [2, 2, 518], [2, 3, 419], [2, 4, 210], [2, 5, 321], [2, 6, 222], [2, 7, 423],[3, 0, 224], [3, 1, 125], [3, 2, 236], [3, 3, 427], [3, 4, 528], [3, 5, 239], [3, 6, 1330], [3, 7, 310],[4, 0, 332], [4, 1, 233], [4, 2, 34], [4, 3, 35], [4, 4, 736], [4, 5, 373], [4, 6, 328], [4, 7, 329],[5, 0, 420], [5, 1, 412], [5, 2, 412], [5, 3, 443], [5, 4, 544], [5, 5, 845], [5, 6, 746], [5, 7, 477],[6, 0, 648], [6, 1, 849], [6, 2, 550], [6, 3, 251], [6, 4, 152], [6, 5, 653], [6, 6, 54], [6, 7, 55]]
    .map(function (item) {
    return [item[0], item[1], item[2] || '-'];
});

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

const heatMapoption = ref({
	gradientColor: [
		"#E5E2F6",
		"#D8D2F1",
		"#BDB3E7",
		"#A194DD",
		"#8675D4",
		"#6B56CA",
		"#4D37B1",
		"#3B2A86",
		"#281D5B",
		"#150F30",
		"#0C081B",
	],
	tooltip: {
		position: "top",
	},
	grid: {
		height: "60%",
		width: "60%",
		left: "center",
		bottom: "0",
	},
	yAxis: {
		type: "category",
		data: hours,
		axisTick: { show: false },
		splitArea: {
			show: true,
		},
		axisLine: {},
	},
	xAxis: {
		type: "category",
		position: "top",
		axisTick: { show: false },
		data: days,
		splitArea: {
			show: true,
		},
	},
	visualMap: {
		type: "piecewise",
		splitNumber: 7,
		itemHeight: 30,
		itemWidth: 20,
		itemSymbol: "rect",
		itemGap: 5,
		min: 0,
		max: 1000,
		calculable: true,
		precision: 0,
		orient: "vertical",
		right: "0",
		bottom: "0%",
		formatter: function (value) {},
	},
	series: [
		{
			name: "View Count",
			type: "heatmap",
			data: data,
		},
	],
});

const maleOption = ref({
	legend: {
		data: [
			{ name: "Male", icon: "rect" },
			{ name: "Female", icon: "rect" },
		],
		bottom: 0,
		left: 20,
		align: "auto",
		itemGap: 20,
	},
	color: ["#f8857d", "#4f8dea"],
	tooltip: {
		trigger: "axis",
		axisPointer: {
			type: "line",
		},
	},
	xAxis: {
		type: "category",
		data: ["10", "20", "30", "40", "50", "60", "70", "80", "90"],
		axisTick: { alignWithLabel: true },
	},
	yAxis: {
		type: "value",
		axisLine: {
			show: true,
		},
		splitLine: { show: false },
	},
	series: [
		{
			name: "Female",
			data: [50, 2000, 2900, 2500, 1800, 1500, 1000, 300, 300],

			type: "line",
			smooth: true,
			showSymbol: false,
		},
		{
			name: "Male",
			data: [50, 1000, 1900, 1500, 1200, 1000, 500, 100, 100],
			type: "line",
			smooth: true,
			showSymbol: false,
		},
	],
});
</script>

<style scoped>
.container {
	width: 500px;
	height: 500px;
}
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
