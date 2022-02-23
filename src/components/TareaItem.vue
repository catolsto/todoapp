<template>
    <div class="alert alert-warning mt-3 d-flex justify-content-between align-items-center">
        <p :class="{'tachado':tarea.estado}">{{ tarea.texto }}</p>
        <div>
            <i @click="Chequear(tarea.id)" 
                class="fa-solid fa-rotate-left mx-2 text-success" 
                role="button"
                v-if="tarea.estado">
            </i>
            <i @click="Chequear(tarea.id)" 
                class="fa-solid fa-circle-check mx-2 text-success" 
                role="button"
                v-if="!tarea.estado">
            </i>
            <i @click="Eliminar(tarea.id)" 
                class="fa-solid fa-circle-minus text-danger" 
                role="button">
            </i>
        </div>
    </div>
</template>

<script>
import { inject } from '@vue/runtime-core'
export default {
    props: [ 'tarea' ],
    setup() {
        const tareas = inject('tareas')
        const Eliminar = (id) => {
            tareas.value = tareas.value.filter(item => item.id !== id)
         }
        const Chequear = (id) => { 
            tareas.value =  tareas.value.map(item => {
                if (item.id === id) {
                    item.estado = !item.estado
                }
                return item
            })
          }

        return { Eliminar, Chequear }
    }

}
</script>

<style scoped>
.tachado {
    text-decoration:line-through;
}
</style>

