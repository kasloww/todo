<script setup>
import {ref, watch} from 'vue'

let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ?? [])
let newtodos = ref('')
let filter = ref('All')

function clicke() {
  todos.value.push({
    text: newtodos.value,
    complete: false
  })
  newtodos.value = ''
}

function getout (index) {
  todos.value.splice(index, 1)
}

function todoFilter (todo) {
  if (filter.value == 'active') {
    return todo.complete == false 
  } else if (filter.value == 'complete'){
    return todo.complete == true
  } else {
    return true
  }
}

function activeFilter (todo) {
  return todo.complete == false
}

watch(todos, function(value) {
  window.localStorage.setItem('todos', JSON.stringify(value))
}, {deep: true})
</script>

<template>
  <div class="centerpls">
  <h1>Hello,</h1>
  <h2>Gonna Forget Something?</h2>
  
  <li v-for="(todo, index) in todos.filter(todoFilter)" :class="{textstuff: todo.complete}">
    <label class="container">
    <input type="checkbox" checked="checked" v-model="todo.complete">
    <span class="checkmark"></span>
    </label>
    {{todo.text}}
    <button @click="getout(index)">🚮</button>
  </li>
  
  <input v-model="newtodos" @keydown.enter="clicke" placeholder="Write here:" class="wherewetype">
  <button @click="clicke" class="enteronly">Enter</button>
  <p></p>

  <div v-if="todos.length > 0">
    <p> {{ todos.filter(activeFilter).length }} remaining.</p>
  <input name="filter" type="radio" value="all" v-model="filter">
  <label>All</label>
  <input name="filter" type="radio" value="active" v-model="filter">
  <label>Active</label>
  <input name="filter" type="radio" value="complete" v-model="filter">
  <label>Completed</label>
</div>
</div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@1,200&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@300&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@200&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300&display=swap');
body {
  background-color: rgb(149, 213, 247, 0.3);
}
.centerpls {
  text-align: center;
}
h1 {
  font-family: 'Montserrat', sans-serif;
  font-weight: 300;
  color:rgb(24, 88, 249)
}
h2 {
  font-family:'Montserrat', sans-serif;
  font-weight: 200;
  color:rgb(24, 88, 249)
}
p {
  font-family:'Montserrat', sans-serif;
  color:rgb(24, 88, 249)
}
button {
    background-color:rgb(255, 255, 255);
    cursor: pointer;
    font-family: 'Raleway', sans-serif;
    border-color: rgba(0, 47, 255, 0.642);
    margin: 8px 0;
    box-sizing: border-box;
}

li {
  font-family: 'Raleway', sans-serif;
  color:rgb(0, 132, 255);
  list-style-type: circle;
}
label {
  font-family: 'Montserrat', sans-serif;
  font-weight: 300;
  color:rgb(24, 88, 249)
}
.wherewetype {
  font-family: monospace;
  width:50%;
  padding: 12px;
  box-sizing: border-box;
}
.enteronly {
  width:5%;
  padding: 12px 20px;
}
.container {
  display: inline-block;
  position: relative;
  padding-left: 30px;
  margin-bottom: 17px;
  cursor: pointer;
  font-size: 10px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: #eee;
}
.container:hover input ~ .checkmark {
  background-color: #ccc;
}
.container input:checked ~ .checkmark {
  background-color: #edf6fc;
}
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}
.container input:checked ~ .checkmark:after {
  display: block;
}
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
.textstuff {
  text-decoration: line-through;
  color: dimgray;
}
</style>
