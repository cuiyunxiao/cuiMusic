<template>
  <div class="hello" ref="mapbox" style="height:400px;width:600px">
   
  </div>
</template>

<script>
// 引入echarts
import echarts from 'echarts';
//引入地图
import 'echarts/map/js/china.js';
const option = {
	title:{
		text:'疫情地图',
		link:'',
		subtext:'',
		sublink:'',
	},
	series:[{	
		type: 'map',
		map:'china',
		label:{//控制地图对应地区
			show:true,
			color:'red',
		}
	}]
}


export default {
  name: 'hello',
 mounted(){
	let myChart =  echarts.init(this.$refs.mapbox);
	console.log(myChart)
	myChart.setOption(option);
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
