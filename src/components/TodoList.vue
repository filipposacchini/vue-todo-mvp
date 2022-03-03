<script setup>
import { ref, computed } from 'vue'
import TodoListItem from './TodoListItem.vue';

let id = 0
const newTodo = ref('')
const todos = ref([])

const activeTodos = computed(() => {
  return todos.value.filter((t) => !t.done)
})

const completedTodos = computed(() => {
  return todos.value.filter((t) => t.done)
})

function addTodo() {
  if (newTodo.value.length > 0) {
    todos.value.push({ id: id++, text: newTodo.value, done: false })
    newTodo.value = ''
  }
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <div class="todoListInput">
    <input class="todoListInput__field input-field" placeholder="Add a new To Do" v-model.trim="newTodo" @keyup.enter="addTodo">
    <button
      class="todoListInput__button button"
      :disabled="newTodo.length === 0"
      @click="addTodo">Add To Do</button>
  </div>
  <div class="todoListWrapper">
    <h3>To Do List <span v-show="activeTodos.length">{{ activeTodos.length }}</span></h3>
    <ul>
      <TodoListItem
        v-for="todo in activeTodos"
        :todo="todo"
        :key="todo.id"
        @remove-todo="removeTodo"
      />
    </ul>
    <div class="todoListWrapper__empty" v-if="!activeTodos.length">Nothing to do here...</div>
  </div>
  <div class="todoListWrapper">
    <h3>Completed <span v-show="completedTodos.length">{{ completedTodos.length }}</span></h3>
    <ul>
      <TodoListItem
        v-for="todo in completedTodos"
        :todo="todo"
        :key="todo.id"
        @remove-todo="removeTodo"
      />
    </ul>
    <div class="todoListWrapper__empty" v-if="!completedTodos.length">This list is empty, yet.</div>
  </div>
</template>

<style lang="scss">
.todoListInput {
  display: flex;
  align-items: stretch;
  margin-bottom: 4rem;

  &__field.input-field {
    border-radius: .375rem 0 0 .375rem;
  }

  &__button.button {
    flex-shrink: 0;
    border-radius: 0 .375rem .375rem 0;
  }
}

.todoListWrapper {
  margin-bottom: 2.5rem;

  &__empty {
    color: var(--light-color);
    font-size: 1.25rem;
    text-align: center;
    padding: 1.5rem 1rem;
    border: 2px dashed var(--light-color);
    border-radius: .75rem;
  }
}
</style>