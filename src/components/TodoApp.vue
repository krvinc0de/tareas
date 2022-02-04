<template>  
    <div>
        <h1 class="my-5 text-center">Proyecto de listas de Tareas</h1>
        <todo-form />
        <todo-list />
    </div>

</template>

<script>
import { provide, ref, watchEffect } from 'vue'
import TodoForm from './TodoForm.vue'
import TodoList from './TodoList.vue'
export default {
    components: {
        TodoForm,
        TodoList
    },
    setup() {
        const tareas = ref([]) //variable global
        provide('tareas', tareas)       

        //si existe la variable de forma local
        if(localStorage.getItem('tareas')){
            tareas.value = JSON.parse(localStorage.getItem('tareas'))
        }
        //parset convertir variable objeto a programacion


        watchEffect( () => {
            localStorage.setItem('tareas', JSON.stringify(tareas.value))
        })
    }
}
</script>