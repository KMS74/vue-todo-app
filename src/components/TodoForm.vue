<template>
  <div class="row w-75 mx-auto my-4 justify-content-between">
    <div class="col-8">
      <input
        class="form-control py-2"
        type="text"
        placeholder="Add todo item"
        v-model="todoTitle"
      />
    </div>
    <div class="col-4">
      <button @click="addTodo" class="btn btn-success">Add Todo</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todoTitle: "",
    };
  },
  methods: {
    addTodo() {
      if (this.todoTitle.length > 0) {
        // emmiting custom event with todoTitle as payload
        this.$emit("onAddTodo", this.todoTitle);
        this.todoTitle = "";
      }
    },
  },
};
</script>

<style scoped></style>
