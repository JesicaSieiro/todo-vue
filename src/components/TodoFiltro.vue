<template>
  <div class="card mt-3 ">
      <div class="card-body d-flex justify-content-between align-items-center">
          <span 
            role="button"
            @click="filtrar('activo')">
              Activos
          </span>
          <span 
            role="button"
            @click="filtrar('all')">
              Todos
          </span>
          <span 
            role="button"
            @click="filtrar('completado')">
              Completados
          </span>

      </div>
  </div>
</template>

<script>
import { inject, ref ,computed, provide} from '@vue/runtime-core'
export default {
    setup(){
        const estado = inject('estado')
        const filtrar = valor => {
            estado.value=valor
        }
        return {filtrar}

        
    }
    

}
</script>

<style>

</style>