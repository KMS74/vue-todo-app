<template>
  <div class="container-md w-75 my-4 mx-auto" v-if="todos.length > 0">
    <!-- Search Bar -->
    <input
      v-if="todos.length > 1"
      class="form-control mt-4 mb-1"
      placeholder="search for todos"
      type="text"
      id="filtetr"
      v-model="filterBy"
    />
    <!-- Check box to show/hide completed todos -->
    <div class="form-check form-check-inline mb-4">
      <input
        class="form-check-input"
        type="checkbox"
        id="hide-completed"
        v-model="hideCompletedTodos"
        :value="hideCompletedTodos"
      />
      <label class="form-check-label" for="hide-completed"
        >{{ hideCompletedTodos ? "Show" : "Hide" }} Completed Todos</label
      >
    </div>
    <div v-if="filteredTodos.length > 0">
      <div
        class="d-flex flex-row justify-content-between align-items-center px-4 bg-ligt shadow-sm p-2 mb-3"
        v-for="todo in filteredTodos"
        :key="todo.id"
      >
        <div class="d-flex gap-4 align-items-center">
          <input
            class="form-check-input m-0"
            type="checkbox"
            v-model="todo.completed"
            :value="todo.completed"
          />

          <p
            :class="[
              todo.completed
                ? 'text-decoration-line-through'
                : 'text-decoration-none',
            ]"
            class="lead m-0"
          >
            {{ todo.title }}
          </p>
        </div>

        <button
          v-on:click="deleteTodo(todo.id)"
          class="btn btn-sm btn-outline-danger"
        >
          <i class="bi bi-trash"></i>
        </button>
      </div>
    </div>
    <p v-else class="lead text-center fs-2 text-danger">Not found todos</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      filterBy: "",
      hideCompletedTodos: false,
    };
  },
  props: {
    todos: {
      type: Object,
      required: true,
    },
  },
  methods: {
    deleteTodo(id) {
      this.$emit("onDeleteTodo", id);
    },
  },
  computed: {
    filteredTodos() {
      this.filterBy.trim().toLowerCase();
      if (this.hideCompletedTodos) {
        return this.todos.filter(
          (todo) =>
            !todo.completed && todo.title.toLowerCase().includes(this.filterBy)
        );
      }
      return this.todos.filter((todo) =>
        todo.title.toLowerCase().includes(this.filterBy)
      );
    },
  },
};
</script>

<style lang="scss" scoped></style>
