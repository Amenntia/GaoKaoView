<template>
  <div class="mylist">
    <ul class="list-group" id='container'>
    
</ul>
  </div>
</template>


<script>
import Type from '../../static/学校层次.json'
import '../../node_modules/bootstrap/dist/css/bootstrap.min.css';
import '../../node_modules/bootstrap/dist/js/bootstrap.min.js';
import PubSub from 'pubsub-js';
export default {
  name: 'HelloWorld',
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
          var container=document.getElementById('container')
          for(let i=0;i<Type.length;i++)
          {
            var li=document.createElement("li");
            li.setAttribute("class","list-group-item");
            
            if(Type[i]['办学层次']=='985')
            {
              var span=document.createElement("span")
              span.setAttribute("class","badge badge-success")
              span.innerHTML+='985'
              li.appendChild(span)
            }
            if(Type[i]['办学层次']=='211')
            {
              var span=document.createElement("span")
              span.setAttribute("class","badge badge-warning")
              span.innerHTML+='211'
              li.appendChild(span)
            }
            li.innerHTML+=Type[i]['学校名称']
            li.onclick=function(){
              var str
              str=this.innerHTML;
              str=str.split('>')
              PubSub.publish("clickSchool",str[str.length-1])
              console.log(str[str.length-1])
            }

            container.appendChild(li)
            
          }
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.mylist{
  width: 440px;
  height: 250px;
  background-color: #145b7d;
}
.list-group{
max-height: 250px; overflow: scroll;
}
.list-group-item{
flex: none;
}
li{
  height: 50px;
  background-color: #145b7d;
}
</style>
