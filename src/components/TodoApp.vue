<template>
    <div class="d-flex justify-content-center">
        <h1>ToDos</h1>
    </div>
    <todo-form/>
    <todo-list />
</template>
<script>
import {ref} from 'vue'
import { provide, watchEffect} from '@vue/runtime-core'
import TodoForm from './TodoForm.vue'
import TodoList from './TodoList.vue'
export default {
  components: { TodoForm , TodoList},
  //aca tenemos que devolver algo
  setup(){
      //construimos un array
      //hacemos una referencia que va a ser un array(tambien se puede hacer con reactive)
      const todos=ref([
       
      ])
       //para pasar la lista y que los componentes hijos puedan acceder.
        // Necesita dos parametros
        //key(un string)y el valor
        provide('todos',todos)

        //RECORDAR => El localStorage vive en el navegador
        //verifica si existe la key de los todos
        //y si existe transformamos el string en array 
        if(localStorage.getItem('todos')){
          todos.value=JSON.parse(localStorage.getItem('todos'))
        }

        //watchEffect recibe una funcion de flecha 
        //lo que hace es estar pendiente de lo que nosotros le digamos
        //automaticamente. Es decir que no necesitamos configurarlo
        watchEffect (()=>{
          //ACLARACION=> al poner los todos por defecto asimila
          //que a ellos es lo que tiene que hacer el seguimiento
    

          //cada vez que se modifiquen los todos guardamos el item 
          //(NECESITAMOS PARSEARLO NUEVAMENTE EN STRING PARA PODER GUARDARLO)
          //y se actualiza el localStorage
        localStorage.setItem('todos',JSON.stringify(todos.value))
        })
  }
    
}
</script>

<style>

</style>