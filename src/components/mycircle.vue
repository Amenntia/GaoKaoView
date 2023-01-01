<template>
    <div>
        <div class="circle" ref="circle"></div>
    </div>
</template>

<script>
import $ from 'jquery'
import Type from '../../static/schoolType.json'
let echarts = require("echarts");
import PubSub from 'pubsub-js';

export default {
  name: 'enter',
  data () {
    return {
        location:'全国',
    }
  },
mounted(){
    this.drawCircle(Type[0]['data']);
    PubSub.subscribe("pub_mapProvince", (msg, data) => {
      this.location = data;
      var temp
      for(let k=0;k<Type.length;k++)
      {
          if(Type[k]['province']==data)
          {
              temp=Type[k]['data']
              break;
          }
      }
      this.drawCircle(temp)
    })
  },
  methods: {
   drawCircle(data){
    // 基于准备好的dom，初始化echarts实例
   var mydata=data
  // console.log(mydata)
    var bar_dv = this.$refs.circle;
    if (bar_dv){
        let myChart = this.$echarts.init(bar_dv)
        var option = {
             title:{
                text: this.location+'高校分类',
                left: "center",
                textStyle: {
                fontSize: 25,
                color: "rgba(245, 237, 237, 1)"//设置标题字体颜色
                 },
            },
        tooltip: {
            trigger: 'item'
    },
    legend: {
        top: '2%',
        right: '1%',
        orient:'vertical',
        textStyle: { //图例文字的样式
                            color: '#fff',
                            fontSize: 16
                        }
    },
    series: [
        {
            name: '访问来源',
            type: 'pie',
            radius: ['40%', '70%'],
            avoidLabelOverlap: false,
            itemStyle: {
                borderRadius: 10,
                borderColor: '#fff',
                borderWidth: 2
            },
            label: {
                show: false,
                position: 'center'
            },
            emphasis: {
                label: {
                    show: true,
                    fontSize: '40',
                    fontWeight: 'bold'
                }
            },
            labelLine: {
                show: false
            },
                data:mydata
        }
    ]
};
      myChart.setOption(option);
}
}}}
</script>

<style scoped>
.circle{
  width: 470px;
  height: 250px;
}
</style>
