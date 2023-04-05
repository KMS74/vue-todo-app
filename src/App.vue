<template>
  <div class="container">
    <h1 class="text-center display-3 my-4">Vuejs Todo App</h1>
    <!-- Todo Form -->
    <TodoForm @onAddTodo="addTodo" />
    <!-- todo list table -->
    <TodoTable @onDeleteTodo="deleteTodo" :todos="todos" />
  </div>
</template>

<script>
import TodoForm from "./components/TodoForm.vue";
import TodoTable from "./components/TodoTable.vue";

export default {
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    addTodo(todoTitle) {
      this.todos.unshift({
        userId: 1,
        id: Date.now(),
        title: todoTitle,
        completed: false,
      });
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id != id);
    },
  },
  created() {
    // fetching todos data from API
    fetch("https://jsonplaceholder.typicode.com/todos")
      .then((response) => response.json())
      .then((todos) => {
        console.log(todos);
        // assining the first 5 toods
        this.todos = todos.filter((todo) => todo.id <= 5);
      })
      .catch((error) => console.log(error));
  },
  components: { TodoForm, TodoTable },
};
</script>

<style scoped></style>
