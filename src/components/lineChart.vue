<template>
    <div v-show="(school!='')&&(location=='')">
        <div class="lineChart" ref="lineChart"></div>
        <div class="barChart" ref="barChart"></div>
    </div>
</template>

<script>
import $ from 'jquery'
import mydata from '../../static/理科历年批次分数2.json'
import wenke from '../../static/文科历年批次分数2.json'
import PubSub from 'pubsub-js'
let echarts = require("echarts");

export default {
  name: 'enter',
  data () {
    return {
        location:'四川',
        school:''
    }
  },
mounted(){
    PubSub.subscribe("clickSchool", (msg, data) => {
      this.school = data;
      this.location=''
      this.drawLineChart(data)
    });
    PubSub.subscribe("pub_mapProvince", (msg, data) => {
       this.school=''
       this.location=data
       
    });
  },
  methods: {
   drawLineChart(schoolName){
    // 基于准备好的dom，初始化echarts实例
    var year 
    var index
    var lineData=[]
    var myLegend=[]
    // console.log(mydata[0][nam])
    for(let j=0;j<mydata.length;j++)
    {
        if(mydata[j]['学校']==schoolName)
        {
            for(let i=0;i<mydata[j]['批次'].length;i++)
            {
                myLegend.push(mydata[j]['批次'][i])
                var nam=mydata[j]['批次'][i]
                year = mydata[j][nam][0]
                var obj={
                    name: nam,
                    type: 'line',
                    stack: '总量',
                    data:mydata[j][nam][1]
                }
                lineData.push(obj)

            }
            index=j
            this.drawBarChart(j)
            break;
        }

    }

     for(let j=0;j<wenke.length;j++)
    {
        if(wenke[j]['学校']==schoolName)
        {
            for(let i=0;i<wenke[j]['批次'].length;i++)
            {
                myLegend.push(wenke[j]['批次'][i])
                var nam=wenke[j]['批次'][i]
                var obj={
                    name: nam,
                    type: 'line',
                    stack: '总量',
                    data:wenke[j][nam][1]
                }
                lineData.push(obj)
            }
            break;
        }

    }

    var bar_dv = this.$refs.lineChart;
        if (bar_dv){
          let myChart = this.$echarts.init(bar_dv)
   var option = {
    title: {
        text: '历年最低录取分数线',
        left: "center",
                textStyle: {
                fontSize: 25,
                color: "rgba(245, 237, 237, 1)"//设置标题字体颜色
                 },
    },
    tooltip: {
        trigger: 'axis'
    },
    legend: {
        data:myLegend,
        bottom:"2%",
        textStyle: { //图例文字的样式
                            color: '#fff',
                            fontSize: 16
                        }
    },
    grid: {
        left: '3%',
        right: '4%',
        bottom: '10%',
        width:'85%',
        containLabel: true
    },
    toolbox: {
        feature: {
            saveAsImage: {}
        }
    },
    xAxis: {
        type: 'category',
         nameTextStyle:{
            fontWeight: "bolder",
            color: "rgba(0, 0, 0, 1)",
            fontSize :12
        },
         axisLine: {
                lineStyle: {
                    color: "#fff",
                }
            },
        boundaryGap: true,
        data: year.reverse()
    },
    yAxis: {
        type: 'value',
        scale:true,
         axisLine: {
                lineStyle: {
                    color: "#fff",
                }
            },
    },
    series: lineData
};
      myChart.setOption(option);
    }
    },

    drawBarChart(item){
        var barData=[]
    // console.log(mydata[0][nam])
    for(let i=0;i<mydata[item]['批次'].length;i++)
    {
        var nam=mydata[item]['批次'][i]
        var obj={
            data:mydata[item][nam][2],
            type: 'bar',
            showBackground: true,
            backgroundStyle: {
                color: 'rgba(180, 180, 180, 0.2)'
            },
            itemStyle: {
            normal: {
　　　　　　　　//这里是重点
                color: function(params) {
                	//注意，如果颜色太少的话，后面颜色不会自动循环，最好多定义几个颜色
                    var colorList = [ '#61a0a8', '#d48265', '#91c7ae','#749f83', '#ca8622'];
                    return colorList[params.dataIndex]
                    }
                }
            }
        }
        barData.push(obj)
    }

    var bar_dv = this.$refs.barChart;
        if (bar_dv){
          let myChart = this.$echarts.init(bar_dv)
   var option = {
        xAxis: {
            type: 'category',
            data:  mydata[item][nam][0],
             axisLine: {
                lineStyle: {
                    color: "#fff",
                }
            },
        },
        yAxis: {
            type: 'value',
             axisLine: {
                lineStyle: {
                    color: "#fff",
                }
            },
        },
        series: barData
    };
      myChart.setOption(option);
    }
    }

}}
</script>

<style scoped>
.lineChart{
  width: 400px;
  height: 270px;
  margin-top: 10%
}
.barChart{
width: 400px;
  height: 270px;
  margin-top: 3%
}
</style>
