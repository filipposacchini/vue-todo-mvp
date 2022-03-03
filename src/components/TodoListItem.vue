<script setup>
const props = defineProps({
  todo: Object
})

const emit = defineEmits(['removeTodo'])
</script>

<template>
  <li class="todoItem">
    <input class="todoItem__toggle" type="checkbox" v-model="todo.done">
    <span class="todoItem__text" :class="{ done: todo.done }">{{ todo.text }}</span>
    <button class="todoItem__button" @click="$emit('removeTodo', todo)"></button>
  </li>
</template>

<style lang="scss">
.todoItem {
  display: flex;
  align-items: center;
  padding: .5rem 1rem;
  margin-bottom: .5rem;
  border-radius: .375rem;
  border: 2px solid var(--light-color);

  &:hover {
    border-color: var(--light-color);
  }

  //&__toggle {}

  &__text {
    flex-grow: 1;
    padding: 0 1rem;
    font-size: 1.125rem;
    line-height: 1.2;
    word-break: break-all;

    &.done {
      text-decoration: line-through;
    }
  }

  &__button {
    width: 1em;
    height: 1em;
    padding: .25rem .25rem;
    color: #000;
    background: transparent url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16' fill='%23000'%3e%3cpath d='M.293.293a1 1 0 011.414 0L8 6.586 14.293.293a1 1 0 111.414 1.414L9.414 8l6.293 6.293a1 1 0 01-1.414 1.414L8 9.414l-6.293 6.293a1 1 0 01-1.414-1.414L6.586 8 .293 1.707a1 1 0 010-1.414z'/%3e%3c/svg%3e") center/1em auto no-repeat;
    border: 0;
    border-radius: .25rem;
    opacity: .5;

    &:hover {
      opacity: 1;
    }
  }
}
</style>