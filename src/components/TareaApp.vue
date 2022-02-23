<template>
    <h1>Tareas APP</h1>
    <tarea-form />
        <tarea-item v-for="tarea in tareas" :key="tarea.id"
          :tarea="tarea" >
        </tarea-item>
    <div v-if="tareas.length  === 0"  class="alert alert-dark mt-3">
        <strong>Sin Tareas Pendientes! 😊</strong>
    </div>

    <p>{{ tareas }}</p>
    
</template>

<script>
import { ref } from '@vue/reactivity'
import { provide, watchEffect } from '@vue/runtime-core'
import TareaForm from './TareaForm.vue'
import TareaItem from './TareaItem.vue'
export default {
  components: { TareaForm, TareaItem },
    setup() {
        const tareas = ref([])
        provide('tareas',tareas)

        // Recupera las tareas de Localstorage
        if (localStorage.getItem('tareas')) {
            tareas.value = JSON.parse(localStorage.getItem('tareas'))
        }
        // Guarda las tareas en el Localstorage cuando cambien las tareas
        watchEffect(() => {
            localStorage.setItem('tareas',JSON.stringify(tareas.value))
        })

        return { tareas }
    }
}
</script>

<style>

</style>