<template>
  <div class="max-w-md mx-auto p-4 bg-white shadow-md rounded">
    <input
      v-model="searchTerm"
      class="w-full p-2 mb-4 border"
      placeholder="Cari tugas..."
    />
    <input
      v-model="newTodo"
      @keyup.enter="addTodo"
      class="w-full p-2 mb-4 border"
      placeholder="Tambahkan tugas"
    />
    <ul>
      <li
        v-for="(todo, index) in filteredTodos"
        :key="index"
        class="flex items-center justify-between py-2 border-b transition-all duration-300 ease-in-out transform hover:scale-105"
      >
        <div class="flex items-center">
          <input type="checkbox" v-model="todo.completed" class="mr-2" />
          <span
            v-if="index !== editIndex"
            :class="{ 'line-through': todo.completed }"
            >{{ todo.text }}</span
          >
          <input
            v-if="index === editIndex"
            v-model="editedText"
            @keyup.enter="saveEdit"
            @keyup.esc="cancelEdit"
            class="border p-2 mr-2"
          />
        </div>
        <div class="flex">
          <button
            @click="editTodo(index)"
            class="p-2 ml-2 bg-blue-500 text-white rounded"
          >
            Edit
          </button>
          <button
            @click="removeTodo(index)"
            class="p-2 ml-2 bg-red-500 text-white rounded"
          >
            Delete
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchTerm: "",
      newTodo: "",
      todos: [],
      editIndex: -1,
      editedText: "",
    };
  },
  computed: {
    filteredTodos() {
      return this.todos.filter((todo) =>
        todo.text.toLowerCase().includes(this.searchTerm.toLowerCase())
      );
    },
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== "") {
        this.todos.push({
          text: this.newTodo,
          completed: false,
        });
        this.newTodo = "";
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(index) {
      this.editIndex = index;
      this.editedText = this.todos[index].text;
    },
    saveEdit() {
      if (this.editIndex !== -1) {
        this.todos[this.editIndex].text = this.editedText;
        this.editIndex = -1;
        this.editedText = "";
      }
    },
    cancelEdit() {
      this.editIndex = -1;
      this.editedText = "";
    },
  },
};
</script>

<style scoped>
.line-through {
  text-decoration: line-through;
}
</style>
