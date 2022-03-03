<script setup>
import TodoList from './components/TodoList.vue';

</script>

<template>
  <header>
    <h1>Vue ToDo MVP</h1>
    <!-- <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" /> -->
  </header>
  <main>
    <div class="wrapper">
      <TodoList />
    </div>
  </main>
</template>

<style lang="scss">
@import './assets/main';
</style>
