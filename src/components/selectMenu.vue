<template>
  <div class="selectMenu" >
    <div id="province" class="dropdown">
        <button type="button" class="btn dropdown-toggle" id="dropdownMenu1" 
			data-toggle="dropdown">
		省市
		<span class="caret"></span>
	</button>
        <ul class="dropdown-menu" id="my-ul" role="menu" aria-labelledby="dropdownMenu1"> </ul>
    </div>
    <div id="type"></div>
    <div id="level"></div>
    <div id='score'></div>
  </div>
</template>


<script>
import '../../node_modules/bootstrap/dist/css/bootstrap.min.css';
import '../../node_modules/bootstrap/dist/js/bootstrap.min.js';
import PubSub from 'pubsub-js';
export default {
  name: 'SelecteMenu',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted(){
    this.drawList()
    },
    methods:{
        drawList()
        {
          var  province=['北京','安徽','福建','甘肃','广东','广西','贵州','海南','河北','河南','黑龙江','湖北','湖南','吉林','江苏','江西','辽宁','内蒙古','宁夏','青海','山东','山西','陕西','上海','四川','天津','西藏','浙江','云南','新疆','重庆']
          
          var oUlProvince=document.getElementById("my-ul")
          for(let i=0;i<province.length;i++)
          {
            var oLiProvince=document.createElement('li')
            oLiProvince.setAttribute("role","presentation")
            oLiProvince.innerHTML='<a role="menuitem" tabindex="-1" href="#">'+province[i]+'</a>'
            oUlProvince.appendChild(oLiProvince)
          }


        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.selectMenu{
    width: 100%;
    height: 100%;
}
.dropdown{
    color: white;
}
</style>
