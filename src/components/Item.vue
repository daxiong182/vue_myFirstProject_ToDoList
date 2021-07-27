<template>
  <div>
    <div class="label">
      <li>
      <input type="checkbox" :checked='todo.done' @change='changeCheck(todo.id)'>
            <span>{{todo.title}}</span> <span class="remove" @click='remove(todo.id)'>×</span>
      </li>
      </div>
    </div>
</template>

<script>
export default {
  name:'Item',
  props:['todo','checkTodo','removel'],
  
  methods: {
    changeCheck:function(id){
      //通知App组件 将对应todo的done值取反
      this.$bus.$emit('checkTodo',id);
      
    },

    remove:function(id){

    if(confirm('确定删除吗？')){

      this.$bus.$emit('removel',id)
      

    }
  },

  },
  
}
</script>

<style scoped>

.label{
  width:90%;
  display: block;
  border: 1px solid #ccc;
  border-radius: 5px;
  height: 32px;
  text-align: left;
  background: #fff;
  line-height: 32px;
  margin-left: 20px;
  margin-bottom: 10px;
  padding-left: 5px;
  position: relative;

}
input:hover{
  cursor: pointer;
}
.label:hover{
  cursor: pointer;
}
.label span{
  font-size: 13px;
  position: absolute;
  top: -1px;
  color:#232323;
}

.label .remove{
  position: absolute;
  right: 2px;
  color: brown;
  width:32px;
  height:32px;
  display: none;
  background: transparent;
}
.label:hover .remove{
  display: block;
}
li{
  list-style: none;
  border-radius: 5px;
}
li:hover{
  background: #eee;
}
</style>