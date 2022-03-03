<script setup>
import { ref } from 'vue'
import TodoList from './TodoList.vue'

let id = 0
let todoId = 0

const newList = ref('')
const lists = ref([
  // { id: id++, title: 'List 1' },
  // { id: id++, title: 'List 2' },
  // { id: id++, title: 'List 3' }
  {
    id: id++,
    title: 'List ZERO',
    todos: [
      { id: todoId++, text: 'Learn HTML', done: true },
      { id: todoId++, text: 'Learn CSS', done: true },
      { id: todoId++, text: 'Learn SASS', done: true },
      { id: todoId++, text: 'Learn JavaScript', done: false },
      { id: todoId++, text: 'Learn Vue', done: false },
      { id: todoId++, text: 'Learn Vite', done: false }
    ]
  }
])

//const selectedList = ref([]);

function createList() {
  if (newList.value.length > 0) {
    lists.value.push({
      id: id++,
      title: newList.value,
      todos: []
    })
    newList.value = ''
  }
}

function deleteList(list) {
  lists.value = lists.value.filter((t) => t !== list)
}

// function selectList(list) {
//   selectedList.value = list;
// }
</script>

<template>

  <label>Add List</label>
  <input class="input-field" v-model.trim="newList" @keyup.enter="createList">
  <button class="button" @click="createList">Create List</button>

  <h3>Lists</h3>
  <ul>
    <li v-for="list in lists" :key="list.id">
     <!-- @click="selectList" -->
      <span>{{ list.title }}</span>
      <button @click="deleteList(list)">X</button>
    </li>
  </ul>
  <hr>

  <TodoList />
   <!-- :todos="selectedList.todos" /> -->

</template>