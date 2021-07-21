<template>
<!--
    role="button" -> hace que se pueda presionar como botones
-->
  <li class="list-group-item d-flex justify-content-between align-items-center">
      <span role="button"
       @click="completado(todo.id)"
       :class="{'tachado':todo.estado}">
          {{todo.texto}}
      </span>
      <span role="button" @click="eliminar(todo.id)">
          <i class="fas fa-times"></i>
      </span>
  </li>
</template>

<script>
import { inject } from '@vue/runtime-core'
export default {
    //recibimos el objeto todo de todoList
    //especificamos el tipo y que es requerido
    props:{
        todo:{
            type:Object,
            required:true

        } 
    },

    setup(){
        const todos= inject('todos')
        
        //NO MOSTRAMOS EL ELEMENTO ELEGIDO
        //filtramos todos los elementos que tengas id diferente
        //por lo tant onos va a mostrar todos los elementos menos el que
        //queremos eliminar
        const eliminar = id =>{
            
            todos.value=todos.value.filter(item=> item.id !== id)
        }
        //TACHAMOS LA TAREA REALIZADA
        //Recorremos los todos para cambiar ese estado
        //->  map genera un nuevo array y lo devuelve (SIEMPRE MAP RETORNA ALGO 
        //-y cuando se retorna tenemos que usar las llaves)
        // con el if identificamos el item dentro de los todos 
        // que sea igual al item que recibimos de la vista (por el id) 
        // y cambiamos el estado
        
        //ACLARACION=> aunque el item  no sea modificado siempre lo devolvemos
        const completado=id=>{
            todos.value=todos.value.map(item=>{
                if(item.id === id){
                    item.estado =true
                }
                return item
            })
        }
        return{eliminar, completado}
    }
}
</script>

<style>
.tachado{
    text-decoration: line-through;
}

</style>