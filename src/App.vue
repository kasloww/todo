<script setup>
import {ref, watch} from 'vue'

let todos = ref(JSON.parse(window.localStorage.getItem('todos')))
let newtodos = ref('')

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

watch(todos, function(value) {
  window.localStorage.setItem('todos', JSON.stringify(value))
}, {deep: true})

</script>

<template>
  <h1>Hello,</h1>
  <p></p>
  <h2>Gonna forget something? Write it here.</h2>
  
  <ul>
  <li v-for="(todo, index) in todos">
    <label class="container">
    <input type="checkbox" checked="checked" v-model="todo.complete">
    <span class="checkmark"></span>
    </label>
    {{ index }}
    {{todo.text}}
    <button @click="getout(index)">❌</button>
  </li>
  

  <input v-model="newtodos" @keydown.enter="clicke">
  <button @click="clicke">Enter</button>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@1,200&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@300&display=swap');
h1, h2 {
  font-family: 'Montserrat', sans-serif;
  color:darkgrey
}
button {
    background-color:rgb(255, 255, 255);
    cursor: pointer;
    font-family: 'Instrument Serif', serif;
    border-color: white;
}
li {
  font-family: 'Oswald', sans-serif;
}
input {
  font-family: monospace;
}
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
  background-color: #2196F3;
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
</style>
