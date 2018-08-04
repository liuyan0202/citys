<template>
  <div>
      <heads></heads>
      <city></city>
      <letter :data="list"></letter>
  </div>
</template>

<script>
import axios from "axios"
import city from "./city"
import letter from "./list"
import heads from "./header"
export default {
  name: 'HelloWorld',
  data () {
    return {
        list:null
    }
  },
  mounted(){
    this.getDate()
  },
  methods:{
    getDate(){
        axios.get("/getCity").then(res=>{
            this.list=res.data.provinceArr;
            console.log(res.data)
        })
    }
  },
  components:{
    letter,heads,city
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h4{
  padding: 5px 10px;
}
.box{
  padding: 5px 10px;
}
</style>
