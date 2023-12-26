<template>
  <div id="app" class="container mx-auto p-4">
    <TodoList />
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  components: {
    TodoList,
  },
};
</script>

<style>
/* Gaya khusus dapat ditambahkan di sini */
</style>
