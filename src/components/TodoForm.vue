<template>
  <form action="" method="post">
    <div class="field">
      <label class="label">Title</label>
      <div class="control">
        <input
          class="input"
          v-model="formTodo.todoTitle"
          type="text"
          placeholder="e.g Market"
        />
      </div>
    </div>

    <div class="field">
      <label class="label">Description</label>
      <div class="control">
        <textarea
          class="textarea"
          rows="6"
          placeholder="e.g. Rice, Dal, Atta"
          v-model="formTodo.todoDescription"
        />
      </div>
    </div>

    <label class="label">Priority:</label>
    <div class="select" :class="priorityColor">
      <select v-model="formTodo.todoPriority">
        <option>High</option>
        <option>Medium</option>
        <option>Low</option>
      </select>
    </div>
    <input
      class="button is-danger is-pulled-right"
      type="submit"
      value="Add"
      @click.prevent="dispatchTodoForAdd"
    />
  </form>
</template>

<script>
export default {
  props: ["addTodo"],
  data() {
    return {
      formTodo: {
        todoTitle: "",
        todoDescription: "",
        todoPriority: "High",
      },
    };
  },
  methods: {
    dispatchTodoForAdd() {
      this.addTodo(this.formTodo);
      this.formTodo.todoTitle = "";
      this.formTodo.todoDescription = "";
    },
  },
};
</script>