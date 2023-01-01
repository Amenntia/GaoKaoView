<template>
    <div class="school" ref="school">
      
    </div>
</template>

<script>
import $ from 'jquery'
import schoolData from '../../static/schoolData.json'
let echarts = require("echarts");

export default {
  name: 'school',
  data () {
    return {
        location:'四川'
    }
  },
mounted(){
    this.drawLine();
  },
  methods: {
   drawLine(){
    var mydata=[]
    console.log(schoolData)
    for(let i =0;i<2754;i++)
    {
        let obj=[];
        obj.push(schoolData[i]['办学层次'])
        obj.push(schoolData[i]['院校类型'])
        obj.push(schoolData[i]['所在地'])
        
        mydata.push(obj)
    }
    console.log(mydata)
    // 基于准备好的dom，初始化echarts实例
    var bar_dv = this.$refs.school;
        if (bar_dv){
          let myChart = this.$echarts.init(bar_dv)
    var option = {
        parallelAxis: [
        {dim: 0, name: '办学层次',type:'category',data:['本科','专科']},
        {dim: 1, name: '院校类型',type:'category',data:['综合','财经','工科','艺术','师范','体育','政法','农业','医药','民族','语言','林业']},
        {dim: 2, name: '所在地',type:'category',data:['北京','安徽','福建','甘肃','广东','广西','贵州','海南','河北','河南','黑龙江','湖北','湖南','吉林','江苏','江西','辽宁','内蒙古','宁夏','青海','山东','山西','陕西','上海','四川','天津','西藏','浙江','云南','新疆','重庆']}
    ],
    series: {
        type: 'parallel',
        lineStyle: {
            width: 1
        },
        data: mydata
    }
};
      myChart.setOption(option);
}
}}}
</script>

<style scoped>
.school{
  width: 1200px;
  height: 400px;
}

</style>
