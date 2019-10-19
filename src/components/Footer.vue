<template>
    <footer class="footer">
        <span class="todo-count">
            <strong>{{todoNum}}</strong>
            <span v-if="todoNum<=1">item left</span>
            <span v-else>items left</span>

        </span>
        <ul class="filters">
            <li>
                <a href="#/all" @click="filterTodo('all')">All</a>
            </li>
            <li>
                <a href="#/active" @click="filterTodo('active')">Active</a>
            </li>
            <li>
                <a href="#/complete" @click="filterTodo('complete')">Complete</a>
            </li>
        </ul>
        <button class="clear-completed" @click="clear">
            Clear commpleted
        </button>
    </footer>



</template>

<script>
    export default {
        name:"Footer",
        computed:{
            //8.使用计算属性来显示todoNum的数量
            todoNum(){
                return this.$parent.todoDatas.filter(value=>{
                    if(value.hasCompleted){
                        return false
                    }else{
                        return true
                    }
                }).length
            }
        },
        methods:{
            //9.点击过滤todoDatas的值
            filterTodo(value){
                this.$parent.view=value
            },
            //11.clear所有的已完成项
            clear(){
                this.$parent.todoDatas=this.$parent.todoDatas.filter(value=>{
                    return !value.hasCompleted
                })
            }
        }
    }
</script>

<style scoped>

</style>