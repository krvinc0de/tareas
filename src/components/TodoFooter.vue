<template>
    <li class="list-group-item d-flex justify-content-between align-items-center">
        <span>
           <span style="color: red; font-size: 20px;"> {{ active.length }} </span> Tareas activas <!--total de tareas activas-->
        </span>
        <span role="button" @click="eliminarCompletados" class="btn btn-danger">
            Eliminar Completadas
        </span>
    </li>
</template>

<script>
import { computed, inject } from 'vue'
export default {
    setup() {
        const tareas = inject('tareas')
        // calcular tareas completadas
        const active = computed ( () => {
            return tareas.value.filter(item => item.estado === false)
        })

        const eliminarCompletados = () => {
            tareas.value = tareas.value.filter(item => !item.estado)
        }

        return {
            active,
            eliminarCompletados
        }
        
    }
}
</script>