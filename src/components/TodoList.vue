<template>
    <div>
    <ul class="list-group">
        <todo-item v-for="item in todos" :key="item.id" :todo="item"/>
        <todo-footer v-if="todos.length" />

        <li v-if="todos.length === 0" class="list-group-item">
            SIN TAREAS PENDIENTES 🤑
        </li>
    </ul>
    <todo-filter />
    </div>
</template>

<script>
//computado, provide para que los hijos utilizen la variable
import { computed,inject, provide, ref } from 'vue'
import TodoItem from './TodoItem.vue'
import TodoFooter from './TodoFooter.vue'
import TodoFilter from './TodoFilter.vue'
export default {
    components: {
        TodoItem,
        TodoFooter,
        TodoFilter
    },
    setup (){
        //solo para este componentes
        const tasks = inject('tareas')
        const estado = ref('all')

        const todos = computed( () =>{
            if(estado.value == 'all'){
                return tasks.value
            }
            if(estado.value == 'active'){
                return tasks.value.filter(item => item.estado === false)
                //hacer filtrados 
            }
            if(estado.value == 'complete'){
                return tasks.value.filter(item => item.estado === true)
                //hacer filtrados 
            }
        })
        provide('estado', estado) //para qque puedan usar 
        return{
            todos
        }
    }

    
}
</script>
