<template>
<div class="body">

<div class="addTask">
  <input type="text" >
  <span @click="addOneTask">New</span>
</div>
<ul class="tabs clearfix">
  <li :class="tabSelected==='ing'&&'active'" @click="menuChange('ing')">...ing</li>
  <li :class="tabSelected==='done'&&'active'" @click="menuChange('done')">done</li>
  <li :class="tabSelected==='all'&&'active'" @click="menuChange('all')">all</li>
</ul>
<div>
  <List :data="listData" @toggleTaskStatus="toggleTaskStatus" @removeTask="removeTask"/>
</div>

</div> 
</template>
<script>
import List from './components/List.vue'

export default {
  data:function(){
    return {
      id:0,
      store:[],
      tabSelected:'ing' //ing , all, done
    }
  },
  computed:{
    listData:function(){
      return this.store.filter((item)=>{
        switch (this.tabSelected) {
          case 'ing':
            return !item.complated
          case 'done':
            return item.complated
          default:
            return true
        }
      });
    }
  },
  methods:{
    menuChange:function(name){
      this.tabSelected=name;
    },
    toggleTaskStatus:function(id){
      let store=this.store;
      for(let item of store){
        if(item.id===id){
          item.complated=!item.complated;
        }
      }
    },
    removeTask:function(id){
      let store=this.store;
      this.store=store.filter((item)=>{
        return item.id!==id
      });
    },
    addOneTask:function(e){
      this.store.unshift({
        id:++this.id,
        name:e.target.previousElementSibling.value,
        complated:false
      });
      e.target.previousElementSibling.value='';
    }
  },
  components:{
    List
  }  
}
</script>
<style>
*{
  margin: 0;
  padding: 0;
}
.clearfix:after{visibility:hidden;display:block;font-size:0;content: " ";clear:both;height:0;}
.clearfix{*zoom:1;}
html,body{
  width: 100%;
  height: 100%;
}
.body{
  width: 100%;
  max-width: 500px;
  overflow: hidden;
  position: relative;
  margin-left: 50%;
  transform: translateX(-50%);
  box-shadow: 0 0 2px 2px #ccc;
  padding: 20px;
}
.addTask{
  vertical-align: top;
}
.addTask input{
  width: 300px;
  font-size: 16px;
  height: 25px;
}
.addTask span{
  margin-left:15px;
  background: #7e9ace;
  color: #fff;
  cursor: pointer;
  display: inline-block;
  box-sizing: border-box;
  padding: 0px 5px;
  height: 29px;
  line-height: 29px;
  border-radius: 5px;
}
.addTask span:hover{
  box-shadow: 0 0 1px 1px #ccc;
}
.tabs{
  list-style: none;
  margin-top: 25px;
}
.tabs li{
  float: left;
  width: 33%;
  text-align: center;
  padding: 8px 0px;
  box-sizing: border-box;
  cursor: pointer;
  background: #ccc;
}
.tabs li:nth-child(2){
  border-left: #fff 1px solid;
  border-right: #fff 1px solid;
}
.tabs .active{
  background: #7e9ace;
  color: #fff;
}
</style>
