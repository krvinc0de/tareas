<template>
    <div class="btn-group d-flex mt-3"
         role="group"
         aria-label="Basic Example">
        <button class="btn btn-success w-100"
                type="button"
                :class="{'text-warning': estado === 'active'}"
                @click="filtro('active')">
            Activos
        </button> 
        <button class="btn btn-warning w-100"
                type="button"
                :class="{'text-danger': estado === 'all'}"
                @click="filtro('all')">
            Todos
        </button>
        <button class="btn btn-primary w-100"
                type="button"
                :class="{'text-info': estado === 'complete'}"
                @click="filtro('complete')">
            Completados
        </button>

    </div>
</template>

<script>
import { computed, inject } from 'vue'
export default {
    setup() {
        const estado = inject("estado")
        const filtro = valor => {
            estado.value = valor
        }
        return {
            estado,
            filtro
        }
        
    }
}
</script>