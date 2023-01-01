<template>
  <div class="mapContainer" ref="chart">
  </div>
</template>

<script>
import $ from 'jquery'
import china from '../../static/china.json'
import location from '../../static/本科学校经纬度.json'
let echarts = require("echarts");
import PubSub from 'pubsub-js';
export default {
  name: 'mymap',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
    }
  },
mounted(){
 
    this.drawLine();
  },
  methods: {
   drawLine(){
    // 基于准备好的dom，初始化echarts实例
    var mydata=location
  //  mydata= [{"name":"清华大学","value":[104.087549,30.40824]},{"name":"北京大学","value":[116.316833,39.998877]},{"name":"复旦大学","value":[121.742955,31.066658]}]
    var bar_dv = this.$refs.chart;
        if (bar_dv){
          //console.log('bar_dv不为空');
          let myChart = this.$echarts.init(bar_dv)
          echarts.registerMap("china", china);

      var option = {
        baseOption: {
          backgroundColor: "#76becc",
          title: {
            text: "全国大学地图",
            x: "center"
          },
          tooltip: {
            show: false
          },
          geo: {
            map: "china",
            center: [108.9199, 33.1904],
            zoom: 4,
            itemStyle: {
              shadowBlur: 5
            },
            roam: true,
            scaleLimit: {
              min: 1,
              max: 15
            }
          },
          //触碰文字
          tooltip: {
            trigger: "item",
          },
          series: [
            {
              type: "scatter",
              coordinateSystem: "geo",
              data: mydata,
              symbolSize: 15,
              label: {
                normal: {
                  show: false
                },
                emphasis: {
                  show: false
                }
              },
              // itemStyle: {
              //   emphasis: {
              //     borderColor: "#FFCC99",
              //     borderWidth: 5
              //   }
              // }
            }
          ]
        }
      };
      myChart.setOption(option);
      myChart.on("click",function(e){
		  //点击地图板块
        if(e.componentType == "geo") {
            PubSub.publish("pub_mapProvince", e["region"]["name"]);
            console.log(e["region"]["name"])
        }
        //点击地图学校点触发订阅事件
        else{
          PubSub.publish("clickSchool", e["data"]["name"]);
          console.log( e["data"]["name"])
        }
      });
}
}}}
</script>

<style scoped>
.mapContainer{
  width: 1000px;
  height: 100%;

}
</style>
