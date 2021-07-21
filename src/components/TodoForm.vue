<template>
  <form @submit.prevent="formulario">
    <!--trim elimina los espacios que esten antes y despues--> 
      <input 
        type="text"
        class="form-control my-3"
        placeholder="Ingrese tarea"
        v-model.trim="texto"
      />
  </form>
</template>

<script>
import { inject , ref } from '@vue/runtime-core'
export default {
    setup(){
        //obtenemos la lista de todos pasandole la  key
        //hace que todo lo que modifiquemos en el inject
        //se refleje en el componente
        const todos=inject('todos')
        const texto=ref('')


        /*siempre que hagamos una funcion en setup y querramos ocuparla en el template
        pongo en el submit del formulario con prevent (@submit.prevent) y siempre hay que 
        retornarlo desde el setup "todo lo que usamos en el template tiene que ser retornado"
        */ 
        const formulario= () => {
            //Validacion de texto vacio
            if(texto.value ===''){
              console.log('texto vacio')
              //return para salir
              return
            }
            //creamos el objeto todo=> una tarea
            /*PROPIEDADES= 
            -> texto de la tarea
            ->estado => false para cuando esta pendientr, true para cuando esta realizada
            -> id-> lo hacemos con la funcion date.now que nos da un numero con la fecha actual
             con milesimas de segundo que no podria repetirse*/
             const todo={
               texto: texto.value,
               estado:false,
               id:Date.now()
             } 
             //empujamos la nueva tarea al array
             todos.value.push(todo)
             //console.log(todos.value)
             //limpiamos el texto del form
             texto.value=''
        }
        return {formulario, texto}
    }
}
</script>

<style>

</style>