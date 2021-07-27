<template>
  <div>
    <div class="box" v-show='this.todos.length'>
    <input type="checkbox" :checked='isAll' @change='checkAll'>
    <span>已完成{{doneTotal}}/全部{{todos.length}}</span>
    <button @click='clearNow'>清除已完成任务</button>
  </div>
  </div>
</template>

<script>
export default {
  name:'MyFooter',
  props:['todos'],
  computed:{
    doneTotal:function(){
      return this.todos.reduce((pre,current)=>{
        return pre+(current.done?1:0)
      },0)

    },
    isAll:function(){
      return this.doneTotal==this.todos.length && this.todos.length>0;
    }
  },

  methods: {

    checkAll(e){
      // console.log(e.target.checked);
      this.$emit("checkAllTodo",e.target.checked);
    },

    clearNow:function(){

    this.$emit("clearAllTodo");

   

  },
     
  },

}

 


</script>

<style scoped>

.box{
  width:90%;
  height: 40px;
  margin-top: 20px;
  font-size: 13px;
  position: relative;
}
input{
  position: absolute;
  left: 27px;
}
span{
  position: absolute;
  left: 52px;
  color: rgb(243, 232, 232);
}
button{
  position: absolute;
  right: -13px;
  top: -5px;
  color: #fff;
  background: rgb(89, 152, 177);
  border: none;
  height: 30px;
  border-radius: 5px;
  cursor: pointer;
}
</style>