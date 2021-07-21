<template>
    <!--
        :todo="todo" => con esto enviamos el todo agregado al componente todoItem
        este todo se refiere al objeto que esa creado en todoForm
    -->
    <ul class="list-group">
        <todo-item 
            v-for="todo in todos" :key="todo.id"
            :todo="todo"
        />
        <li 
            v-if="todos.length ===0"
            class="list-group-item"
        >
                No hay tareas pendientes
        </li>
       <todo-footer
                v-if="todos.length !==0"
       />

       <todo-filtro/>
    </ul>
</template>

<script>
import { inject , ref ,computed} from '@vue/runtime-core'
import { provide} from '@vue/runtime-core'
import TodoItem from './TodoItem.vue'
import TodoFooter from './TodoFooter.vue'
import TodoFiltro from './TodoFiltro.vue'
export default {
  components: { TodoItem , TodoFooter , TodoFiltro},
  setup(){
      const todosTodos = inject ('todos')

      const estado = ref('all')

      //propiedad computada
      const todos= computed(()=>{
          if(estado.value==='all'){
            return todosTodos.value
          }
          if(estado.value==='activo'){
              return todosTodos.value.filter(item => item.estado===false)
          }
          if(estado.value === 'completado'){
              return todosTodos.value.filter(item=>item.estado===true)
          }

         
                                                
      })
        //cambiamos el estado , pasando algo reactivo a un componente secundario
        //usando provide (que funciona de un componente principal a un componente hijo)
        provide('estado', estado)
      return{todos}
  }

}
</script>

<style>

</style>