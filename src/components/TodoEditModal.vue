<template>
  <div class="modal" :class="{ 'is-active': active }">
    <div class="modal-background" @click="deactivate"></div>
    <div class="modal-content">
      <form action="" method="post">
        <div class="field">
          <label class="label has-text-white">Title</label>
          <div class="control">
            <input
              class="input"
              v-model="updatedFormTodo.todoTitle"
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
              v-model="updatedFormTodo.todoDescription"
            />
          </div>
        </div>
        <input
          class="button is-danger is-pulled-right"
          type="submit"
          value="Update"
          @click.prevent="dispatchTodoForUpdate"
        />
      </form>
    </div>
    <button
      class="modal-close is-large"
      aria-label="close"
      @click="deactivate"
    ></button>
  </div>
</template>

<script>
export default {
  props: ["filler", "active", "deactivate", "updateTodoCard"],
  data() {
    return {
      updatedFormTodo: {
        todoTitle: this.filler.todoTitle,
        todoDescription: this.filler.todoDescription,
      },
    };
  },
  methods: {
    dispatchTodoForUpdate() {
      this.updateTodoCard({
        todoIndex: this.filler.todoIndex,
        todoTitle: this.updatedFormTodo.todoTitle,
        todoDescription: this.updatedFormTodo.todoDescription,
        todoCreationTime: this.filler.todoCreationTime,
      });
      this.deactivate();
    },
  },
};
</script>

