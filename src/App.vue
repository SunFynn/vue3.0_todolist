<template>
<div>
  <section class="todoapp">
      <header class="header">
          <h1>Todos</h1>
          <input type="text" class="new-todo" v-model="newTodo" @keyup="addTodo"/>
      </header>
      <section class="main">
        <input type="checkbox" class="toggle-all" v-model="isAll"/>
        <ul class="todo-list">
            <Item v-for="value in filterTodos()" :key="value.id" :todo="value"/>
        </ul>
      </section>
      <Footer/>
      
      
  </section>
  <div class="div"></div>
</div>
</template>

<script>
import Item from "@/components/Item";
import Footer from "@/components/Footer";
import "./css/index.css"
export default {
  name: 'App',
  components:{Item,Footer},
  data(){
    return{
       todoDatas:[],
       newTodo:'',
       view:'all'
    }
  },
  methods:{
    //1.添加todo项
    addTodo(){
      if(this.newTodo.trim()!=''){
        let todo={};
        todo.id=new Date().getTime();
        todo.value=this.newTodo;
        todo.hasCompleted=false;
        this.todoDatas.push(todo);
        this.newTodo=""
      }
    },
    //9.过滤tododatas，判断显示
     filterTodos(){
      switch(this.view){
        case "all":return this.todoDatas;
        case "active":return this.todoDatas.filter(value=>{
          return !value.hasCompleted
        });
        case "complete":return this.todoDatas.filter(value=>{
          return value.hasCompleted
        });
      }
    }
  },
  computed:{
    //10.全选或者全不选
    isAll:{
      get(){
          return this.$children.todoNum==0
      },
      set(value){
          this.todoDatas.map(todo=>{
            todo.hasCompleted=value;
            return value
          })
      }
    }
  }
}
</script>

<style>
    .div{
      width:50px;
      height: 50px;
      background: red;
      transform: scale(1,1) rotate(0deg);
      /* transform: rotate(0deg); */
      transition: transform 1s ease 0s;
    }
    .div:hover{
      transform:scale(5,5) rotate(3600deg);
      /* transform: rotate(3600deg); */
    }
</style>
