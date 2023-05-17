<script setup> 
import {ref, watch} from "vue" 
 let filter=ref("all")
 

 let todos= ref(JSON.parse(window.localStorage.getItem("todos")) ?? [])

  watch(todos,function(value) {
    window.localStorage.setItem("todos",JSON.stringify(value))
  }, {deep:true}) 

  function todoFilter (todo) {
    if(filter.value=="active") {
      return todo.complete== false

    }
    else if(filter.value=="completed") {
      return todo.complete== true
    }
    else {
      return true
    }
  }

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
  <input name="filter" type="radio" value="all" v-model="filter"> 
  <label>All</label>
  <input name="filter" type="radio" value="active" v-model="filter">
 <label>Active</label> 
 <input name="filter"  type="radio" value="completed" v-model="filter">
 <label>Completed</label>
  <h1>My Todo List</h1>  
  <ul class="dripster">
  <li v-for="(todo, index) in todos.filter(todoFilter)">
    <label class="container"><input type="checkbox" v-model="todo.complete"><span class="checkmark"></span></label>
    
    <button @click="deleteTodo(index)">🗑</button> 

    <span :class="{completed: todo.complete}">{{ todo.text }}</span>

  <button @click="deleteTodo()">🗑</button>
  </li> 
  </ul> 
  <input v-model="newtodo" class="button " @keydown.enter="popUpTodo">
  <button @click="popUpTodo" class="button">Add Todo</button>
</template>

<style> 
@import url('https://fonts.googleapis.com/css2?family=Shadows+Into+Light&display=swap');

body{
  background-color: bisque; 
  font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif; 


}
/* Customize the label (the container) */
.container {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: #eee;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: #ccc;
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #2196F3;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
} 
.completed {
  text-decoration: line-through; 
  color:#ccc
} 
.dripster {
  background-color: beige; 
  border-radius: 200px;
} 

.button {
  background-color: #b1731c; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px; 
  border-radius: 20px;
}

</style>