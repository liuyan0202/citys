<template>
  <ul class="list">
    <li v-for="(item,index) in data" :key="index">
      <h5>{{item.letter}}</h5>
      <span v-for="(citys,index) in item.province" @click="check(citys.name)" :key="index">
        {{citys.name}}
      </span>
    </li>
  </ul>
</template>
<script>
export default {
  data(){
    return{
      active:false
    }
  },
  props: ["data"],
  mounted(){
       bus.$on("sendcity",(msg)=>{
          let el=this.$el.children;
          [...el].map(item=>{
            [...item.children].map(item=>{
              // console.log(item.innerHTML)
              if(item.innerHTML.trim()==msg){
                item.classList.remove("active")
              }
            });
          });
       });
  },
  methods:{
    check(msg){
      bus.$emit("sendMsg",msg)
      let el=this.$el.children;
      [...el].map(item=>{
        [...item.children].map(item=>{
           // console.log(item.innerHTML)
           if(item.innerHTML.trim()==msg){
             item.classList.add("active")
           }
        });
      });
    }
  }
}
</script>
<style>
.list li{
  padding: 0 10px;
}
.list li h5 {
  height: 30px;
  line-height: 30px;
}
.list li span{
  padding: 2px;
  margin: 10px;
  cursor: pointer;
}
.active{
  border:1px solid yellow;
}
</style>


