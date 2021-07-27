<template>
  <div>
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" @keyup.enter='addToDo' v-model="title">
  </div>

</template>

<script>
import {nanoid} from 'nanoid';
export default {
  name:'MyHeader',
  data() {
    return {
      title:'',
    }
  },
  


  methods: {

    addToDo:function(){

      if(!this.title.trim()){
        return alert('输入不能为空')
      }
      //将用户的输入包装成为一个todo对象
      const todo={id:nanoid(),title:this.title,done:false};

      this.$emit("addToDo",todo);

      this.title='';
      
      
    }
  },
}



</script>

<style scoped>


input{
  width: 90%;
  margin-top: 10px;
  margin-bottom:20px;
  padding-left: 5px;
  border-radius: 5px;
  height: 30px;
  outline: none;
  border: 1px solid #c6c6c6;
  
}



</style>