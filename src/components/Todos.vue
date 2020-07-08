<template>
    <div>
         <h3>Todos</h3>
         <div class="legend">
             <span>Double Click to mark as Complete</span>
             <span>
                 <span class="incomplete-box"></span> = incomplete
             </span>
             <span>
                 <span class="complete-box"></span> = Complete
             </span>
         </div>
         <div class="todos" >
             <div
              v-for="todo in allTodos"
              v-bind:key="todo.id"
              @dblclick="ondbclick(todo)"
              v-bind:class="{'is-complete':todo.completed}"
              class="todo">
                {{todo.title}}
                <i class="fas fa-trash" @click="deleteTodo(todo.id)"></i>
             </div>
         </div>
    </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex';
export default {
    name:"Todos",
    methods:{
        ...mapActions(['fetchTodos', 'deleteTodo', 'updateTodo']),
        ondbclick(todo){
            const updtodo ={
                id:todo.id,
                title:todo.title,
                completed : !todo.completed
            }

            this.updateTodo(updtodo)
        }
    },
    created(){
     this.fetchTodos()
    },
    computed:mapGetters(['allTodos'])
}
</script>

<style scoped>
.todos{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 1rem;
}

.todo{
    border:1px solid #ccc;
    background: #41b883;
    padding: 1rem;
    border-radius: 5px;
    text-align: center;
    position: relative;
    cursor: pointer;
}

i{
    position: absolute;
    right: 10px;
    bottom: 10px;
    color: #fff;
    cursor: pointer;
}

.legend{
    display: flex;
    justify-content: space-around;
    margin-bottom: 1rem;
}

.complete-box{
    display: inline-block;
    width: 10px;
    height: 10px;
    background: #35495e;
}

.incomplete-box{
    display: inline-block;
    width: 10px;
    height: 10px;
    background:#41b883;
}

.is-complete{
    background: #35495e;
    color: #fff;
}
</style>