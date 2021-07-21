<template>
  <li class="list-group-item d-flex justify-content-between align-items-center">
      <span 
            role="button"
       >
            {{contarActivos}} activos
      </span>
      <span role="button" @click="eliminarCompletado">
          Eliminar Completados
      </span>
  </li>
</template>

<script>
import { computed, inject } from '@vue/runtime-core'
export default {
    setup (){
        const todos=inject('todos')

        //para contar as tareas activas vamos a usar una propiedad computada
        //recibe una función de flecha y siempre retorna algo
        //es este caso retorna el nuemro de los todos con estado en falso
        const contarActivos=computed(()=>{
            return todos.value.filter(item=> item.estado ===false).length
        } )

        const eliminarCompletado=()=>{
            //devolvemos los que todavia estan activos, 
            //(es decir los que todavia no fueron hechos y el estado es false)
            //para que el usuario solo vea los que le quedam por hacer
            todos.value=todos.value.filter(item=>item.estado===false)

        }

        return {contarActivos, eliminarCompletado}
    }

}
</script>

<style>

</style>