<script setup>
 import {ref} from "vue" 

 let todos= ref([]) 
 let newtodo= ref("") 
 function popUpTodo () {
  todos.value.push({
    text: newtodo.value, 
    complete: false 
  })

  newtodo.value=""

 } 
 function deleteTodo(index) { 
  todos.value.splice(index,1)

 }
</script>

<template>
  <h1>My Todo List</h1> 
  <ul>
  <li v-for="(todo, index) in todos"> 
    <input type="checkbox" v-model="todo.complete">
    <button @click="deleteTodo(index)">🗑</button> 

  {{ todo.text }} 
  </li> 
  </ul> 
  <input v-model="newtodo" @keydown.enter="popUpTodo">
  <button >Add Todo</button>
</template>

<style> 
body{
  background-color: bisque; 
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif; 


}


</style>
