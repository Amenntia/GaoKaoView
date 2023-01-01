<template>
   <div class="app">
           <!-- <div class="head">head</div> -->
           <div class="container">
                <div class="left">
                    <div style="width:300px">
                        <my-select-menu></my-select-menu>
                    </div>
                </div>
                <div class="mid">
                  <mymap></mymap>
                </div>
                <div class="right">
                    <enterScore class= "box"></enterScore>
                    <my-line-chart></my-line-chart>
                </div>
           </div>
           <div class="foot">
               <mycircle class= "box" style="width:28%; height:auto; float:left; display:inline"></mycircle>
                <mycircle2 class= "box" style="width:25%;  height:auto; float:left; display:inline"></mycircle2>
                <my-list class= "box" style="width:24%;  height:auto; float:left; display:inline"></my-list>
                <my-world-cloud  class= "box" style="width:23%;  height:100%; float:left; display:inline">></my-world-cloud> -->
               <!-- <school-para></school-para> -->
           </div>
      </div>

</template>

<script>
import mymap from './components/map';
import enterScore from './components/enterScore';
import schoolPara from './components/schoolPare';
import mycircle from './components/mycircle';
import mycircle2 from './components/mycircle2';
import myList from './components/myList';
import myWorldCloud from './components/worldCloud';
import myLineChart from './components/lineChart';
import mySelectMenu from './components/selectMenu';
export default {
  name: 'App',
  components:{
    mymap,
    enterScore,
    schoolPara,
    mycircle,
    mycircle2,
    myList,
    myWorldCloud,
    myLineChart,
    mySelectMenu
    },
    data: function () {
      return {
      }
    }
}
</script>

  <style>
        /* 三栏布局，中间自适应高度... */
        * {
            margin: 0;
            padding: 0;
        }    
        /* .head{
            height: 100px;
            width: 100%;
            background-color: gold;
            text-align: center;
        } */
        .app{
           background-color: #145b7d;
        }
        .container{
            position: absolute;
            width: 100%;
            display: flex;
            top: 0px;
            bottom: 30%;
        }
        .left{
            width: 30%;
            background-color: #145b7d;
            text-align: center;
        }
        .right{
            width: 34%;
            background-color: #145b7d;
            text-align: center;
        }
        .mid{
            flex: 1;
            text-align: center;
        }
        .foot{
            position: absolute;
            width: 100%;
            height: 30%;
            bottom: 0;
            background-color: #145b7d;
            text-align: center;
        }
        .box{
            box-shadow: 0px 0px 20px #333399;
            border-style:outset
        }


</style>
