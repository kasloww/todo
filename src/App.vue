<script setup>
import {ref} from 'vue'

let todos = ref([])
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


</script>

<template>
  <h1>What Do You Need Done Today?</h1>
  
  <ul>
  <li v-for="(todo, index) in todos">
    <input type="checkbox" v-model="todo.complete">
    <button @click="getout(index)">❌</button>
    {{ index }}
    {{todo.text}}
  </li>
  </ul>

  <input v-model="newtodos" @keydown.enter="clicke">
  <button @click="clicke">Add Todo</button>
</template>

<style>
h1 {
  text-decoration: underline;
  font-family: 'Times New Roman', Times, serif;
}
button {
    background-color:aliceblue;
    color:blue;
    cursor: pointer;
    font-family: 'Instrument Serif', serif;
}
li {
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}
input {
  font-family: monospace;
}
</style>
