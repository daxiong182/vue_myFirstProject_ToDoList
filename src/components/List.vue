<template>
   
  <div class="list">

    <transition-group
     name="animate__animated animate__bounce animate__repeat-2"
     enter-active-class="animate__bounceInDown"
     leave-active-class="animate__backOutDown"
    
    >
     <item v-for='todo in todos' :key='todo.id' :todo='todo' ></item>
    </transition-group>
   
    
  </div>
</template>

<script>
import 'animate.css'
import Item from './Item.vue';

export default {
  name:'List',
  components:{
    Item,
  },
  props:['todos'],
  
  data() {
    return {
      
    }
  },
}
</script>

<style scoped>
.list{
  width: 100%;
}
</style>