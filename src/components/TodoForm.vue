<template>
    <form class="fromulario" @submit.prevent="agregarTarea"> <!-- evitar refresh  -->
        <input type ="text" 
                placeholder="Create a new task" 
                class="form-control my-2"
                v-model.trim = "texto"
        >
    </form>
</template>


<script>
import { inject, ref, toRef } from 'vue'
export default {
    setup() {
        const tareas = inject('tareas')
        const texto = ref('')

        const agregarTarea = () => {
            //revisar si hay escrito algo
            if(texto.value === ''){
                alert('Tarea Vacia')
                return
            }

            const tarea = {
                id: Date.now(),
                texto: texto.value,
                estado: false
            }
            //console.log(tarea)
            texto.value = ''

            tareas.value.push(tarea)
            console.log(tarea)
        }
        return{
            texto, 
            agregarTarea
        }
    }
    
}
</script>


<style scoped>
.formulario {
    border-width: 1px;
    border-color: blue;
    border-radius: 5px;
    border-style: solid;
    width: 100%;
}
    
.inputText {
    margin-left: 0px;
}
</style>