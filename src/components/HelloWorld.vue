<template>
	<div class="hello" ref="mapbox" style="height:800px;width:1000px">

	</div>
</template>

<script>
	// 引入echarts
	import echarts from 'echarts';
	//引入地图
	import 'echarts/map/js/china.js';
	import jsonp from 'jsonp';
	const option = {
		title: {
			text: '疫情地图',
			link: '',
			subtext: '',
			sublink: '',
		},
		series: [{
			name: '确诊人数',
			type: 'map',
			map: 'china',
			label: { //控制地图对应地区
				show: true,
				color: '#333',
				fontSize: 10
			},
			itemStyle: {
				areaColor: 'white',
				borderColor: 'gray'
			},
			roam: true,
			zoom: 1.2,
			emphasis: {
				//设置鼠标滑动样式
				label: { //控制地图对应地区

					color: '#fff',
					fontSize: 12
				},
				itemStyle: {
					areaColor: '#70ade9',
					borderColor: 'gray'
				},
			},
			data: [
				//后台数据

			]
		}],
		visualMap: [{ //视觉映射组件
			type: 'piecewise',
			show: true,
			pieces: [{
					min: 10000
				},
				{
					min: 1000,
					max: 9999
				},
				{
					min: 100,
					max: 999
				},
				{
					min: 10,
					max: 99
				},
				{
					min: 1,
					max: 9
				},
			],
			inRange: {
				symbol: 'rece',
				color: ['#ffc0b1', '#9c0505']
			}
		}],
		tooltip: { //鼠标滑动详情
			trigger: 'item'
		},
		toolbox: {
			show: true,
			orient: 'vertical',
			left: 'right',
			top: 'center',
			feature: {
				dataView: {
					readOnly: false
				},
				restore: {},
				saveAsImage: {}
			}
		}
	}


	export default {
		name: 'hello',
		mounted() {
			this.myChart = echarts.init(this.$refs.mapbox);
			this.myChart.setOption(option);
			this.getData();
		},
		methods: {
			getData() {
				jsonp('https://interface.sina.cn/news/wap/fymap2020_data.d.json?_=1580892522427', {}, (err, data) => {
					if (!err) {
						console.log(data)
						let list = data.data.list.map(item => ({
							name: item.name,
							value: item.value
						}))
						option.series[0].data = list;
						this.myChart.setOption(option);

					}
				})
			}
		}

	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	h3 {
		margin: 40px 0 0;
	}

	ul {
		list-style-type: none;
		padding: 0;
	}

	li {
		display: inline-block;
		margin: 0 10px;
	}

	a {
		color: #42b983;
	}
</style>
