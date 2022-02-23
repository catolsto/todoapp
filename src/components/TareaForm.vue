<template>
    <form @submit.prevent="agregarTarea">
        <div class="form-group mb-1">
          <label for="">Tarea</label>
          <input type="text"
            class="form-control" 
            placeholder="Ingresa laTarea"
            v-model.trim="texto"
            >
        </div>
        <button class="btn btn-primary btn-lg w-100">Agregar Tarea</button>
    </form>
</template>

<script>
import { inject, ref } from '@vue/runtime-core'
export default {
    setup() {
        const texto = ref('')
        const tareas = inject('tareas')

        const agregarTarea = () => {
            if (texto.value === '') {
                console.log('Texto Vacio!!')
                return
            }
            const tarea = { 
                texto: texto.value,
                estado: false,
                id: Date.now()
                }

            tareas.value.push(tarea)
            texto.value = ''
        }

        return { agregarTarea, texto  }
    }
}
</script>

<style>

</style>