<template>
    <div>
        <h4>您已选择城市</h4>
        <div class="box">
            <span>北京</span>
            <span v-for="item in arr" @click="deletes(item)" :key="item" >
                {{item}}
            </span>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            arr:[]
        }
    },
    mounted(){
         bus.$on("sendMsg",(msg)=>{
             if(this.arr.indexOf(msg)==-1){
                  this.arr.push(msg)
             }
            
         })
    },
    methods:{
        deletes(msg){
          this.arr.map((item,index)=>{
            if(item==msg){
                this.arr.splice(index,1)
            }
          });
           bus.$emit("sendcity",msg)
        }
    }
}
</script>
<style scoped>
h4{
  padding: 5px 10px;
}
.box{
  padding: 5px 10px;
}
.box span{
    cursor: pointer;
}
</style>


