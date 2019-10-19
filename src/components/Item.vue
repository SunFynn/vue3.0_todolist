<template>
     <li :class="{completed:todo.hasCompleted,editing:edit}">
        <div class="view">
            <input type="checkbox" class="toggle" @change="changeHasComplete(todo)"/>
                                                                                      <!-- v-model="todo.hasCompleted" -->
                                                   <!-- 方法一绑定change函数  -->  <!-- 方法二v-model绑定hasCompleted项  -->
            <label @dblclick="editTodo">                             
                {{todo.value}}
            </label>
            <button class="destroy" @click="removeTodo(todo)"></button>
        </div>
        <input type="text" class="edit" v-model="editedTodo.value" 
                                        v-focus="editedTodo===todo"   
                                        @blur="changeEdit"
                                        @keyup.enter="changeEdit"
                                        @keyup.esc="noChange"
        /> 
        <!-- v-focus为true，执行自定义v指令 -->
    </li>

</template>

<script>
    export default {
        name:"Item",
        data(){
            return {
                edit:false,
                editedTodo:'',
                oldTodo:''
            }
        },
        props:{
            todo:Object
        },
        methods:{
            //2.删除todo项，通过$parent就可以获取到父组件的内容，就可以改变父组件的内容
            removeTodo(todo){
                 this.$parent.todoDatas=this.$parent.todoDatas.filter(value=>{
                     if(todo.id===value.id){
                         return false
                     }else{
                         return true
                     }
                 })
            },
            //3.改变todo项的状态，方法一：通过$parent改变父组件的hasCompleted的状态
            changeHasComplete(todo){
                this.$parent.todoDatas=this.$parent.todoDatas.map(value=>{
                    if(value.id===todo.id){
                        value.hasCompleted=!value.hasCompleted
                    }
                    return value
                })
            },
            //4.改变todo的值
            editTodo(){
                this.edit=true;
                this.editedTodo=this.todo;
                this.oldTodo=this.editedTodo.value
            },
            //6.失去焦点和enter键都改变这项todo的值
            changeEdit(){
                this.edit=false;
                this.todo.value=this.editedTodo.value
            },
            //7.esc不改变todo项的value值
            noChange(){
                this.edit=false;
                this.todo.value=this.oldTodo
            }
            
        },
        directives:{
            //5.自定义一个v指令，双击改变edit之后，获得到焦点
            focus(el){
               el.focus()
            }
        }
        
    }
</script>

<style scoped>

</style>