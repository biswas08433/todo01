<template>
  <form action="" method="post">
    <div class="field">
      <label class="label has-text-white">Title</label>
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
      <label class="label has-text-white">Description</label>
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
    <button
      class="button is-danger is-pulled-right"
      @click.prevent="emitSubmitted"
    >
      {{ formAction }}
    </button>
  </form>
</template>

<script>
export default {
  // Props: fillerData, formAction
  props: {
    fillerData: {
      type: Object,
      default: function () {
        return {
          todoTitle: "",
          todoDescription: "",
          todoPriority: "High",
        };
      },
    },
    formAction: {
      type: String,
      default: "Add",
    },
  },

  computed: {
    priorityColor: function () {
      return "is-info";
    },
  },
  data: function () {
    return {
      formTodo: {
        todoTitle: this.fillerData.todoTitle,
        todoDescription: this.fillerData.todoDescription,
        todoPriority: this.fillerData.todoPriority,
      },
    };
  },
  watch: {
    fillerData(newValue) {
      console.log(newValue);
      this.formTodo = {
        todoTitle: newValue.todoTitle,
        todoDescription: newValue.todoDescription,
        todoPriority: newValue.todoPriority,
      };
    },
  },
  methods: {
    emitSubmitted: function () {
      this.$emit("submitted", this.formTodo, this.fillerData.todoIndex);
      this.formTodo = {
        todoTitle: this.fillerData.todoTitle,
        todoDescription: this.fillerData.todoDescription,
        todoPriority: this.fillerData.todoPriority,
      };
    },
  },
};
</script>