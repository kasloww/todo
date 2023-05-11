<script setup>
import {ref} from 'vue'

let todos = ref([])
let newtodos = ref('')

function clicke() {
  todos.value.push(newtodos.value)

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
    <button @click="getout(index)">❌</button>
    {{ index }}
    {{todo}}
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
    background-color:darkblue;
    color:azure;
    cursor: pointer;
    font-family: 'Instrument Serif', serif;
}
li {
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
}
</style>
