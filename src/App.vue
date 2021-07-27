<template>
  <div id="app">
    <div class="box">
    <h3>To Do List</h3>
    <my-header @addToDo='addToDo'></my-header>
    <list :todos='todos' ></list>
    <my-footer @checkAllTodo='checkAllTodo' :todos="todos" @clearAllTodo='clearAllTodo'></my-footer>
    </div>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue';
import MyFooter from './components/MyFooter.vue';
import List from './components/List.vue';
export default {
  name: 'App',
  components: {
   MyHeader,
   MyFooter,
   List,
  },



data() {
  return {
   todos:JSON.parse(localStorage.getItem('todos'))||[]
  }
},


methods: {
  addToDo(todo){
  this.todos.unshift(todo); 
  },

  checkTodo(id){
  this.todos.forEach((todos)=>{
    if(todos.id===id){
      todos.done=!todos.done
    }
  })
},
  deleteTodo(id){
 this.todos = this.todos.filter((todo)=>{
    return todo.id!==id;
  })
},
checkAllTodo(done){
  this.todos.forEach((todo)=>{
    todo.done=done;
  })
  
},
clearAllTodo(){
 this.todos= this.todos.filter((todo)=>{
    return !todo.done
  })
}


},
watch:{

  todos:{
    deep:true,
    handler(value){
      localStorage.setItem('todos',JSON.stringify(value));
    },
    
  }
  
},
mounted(){
  this.$bus.$on('removel',this.deleteTodo);
  this.$bus.$on('checkTodo',this.checkTodo);
},
beforeDestroy() {
  this.$bus.$off(['removel','checkTodo']);
},



}




</script>

<style scoped>


#app{
width: 100%;
min-height: 1080px;
overflow: hidden;
background: url('./assets/003.jpeg') no-repeat center center;
background-size: cover;

}
.box{
width: 460px;
 border:1px solid #ccc;
  text-align: center;
  box-shadow: 0 0 5px rgb(126,188,217);
   border-radius: 5px;
   background: linear-gradient(to bottom,rgb(85,150,180) 5%,rgb(50,79,95) 85%,rgb(47,104,141) 100%);
   opacity: 0.8;
    margin: 125px auto 0px;
}
h3{
  color: rgb(243, 232, 232);
  margin-bottom:5px;
}



</style>
