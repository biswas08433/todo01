<template>
  <div class="card m-4" :class="cardPriority">
    <header class="card-header">
      <p class="card-header-title" :class="cardTextColor">
        {{ todoData.todoTitle }}
      </p>
      <button class="card-header-icon" aria-label="more options">
        <span class="icon">
          <i class="fas fa-angle-down" aria-hidden="true"></i>
        </span>
      </button>
    </header>
    <div class="card-content">
      <div
        class="content is-size-6 is-flex is-flex-direction-column is-justify-content-space-between"
      >
        <!-- {{ todoData.todoIndex }} -->
        <!-- <div class="card-content-inner"> -->
        {{ todoData.todoDescription }}

        <br />
        <time
          class="is-size-7 inter-400 is-align-self-flex-end"
          datetime="2016-1-1"
          >{{ todoData.todoCreationTime }}</time
        >
        <!-- </div> -->
      </div>
    </div>
    <footer class="card-footer">
      <a
        href="#"
        class="card-footer-item"
        :class="cardTextColor"
        @click.prevent="() => (editModalActive = true)"
        >Edit</a
      >
      <a
        href="#"
        class="card-footer-item"
        :class="cardTextColor"
        @click.prevent="deleteTodoCard(todoData.todoIndex)"
        >Delete</a
      >
    </footer>
  </div>
  <TodoEditModal
    :filler="todoData"
    :active="editModalActive"
    :deactivate="() => (editModalActive = false)"
    :update-todo-card="updateTodoCard"
  />
</template>

<script>
import TodoEditModal from "@/components/TodoEditModal.vue";

export default {
  props: ["todoData", "deleteTodoCard", "updateTodoCard"],
  computed: {
    cardPriority: function () {
      switch (this.todoData.todoPriority) {
        case "High":
          return "high-priority";
          break;
        case "Medium":
          return "medium-priority";
        case "Low":
          return "low-priority";
        default:
          break;
      }

      return "";
    },
    cardTextColor: function () {
      switch (this.todoData.todoPriority) {
        case "High":
          return "has-text-danger";
          break;
        case "Medium":
          return "has-text-warning";
        case "Low":
          return "has-text-info";
        default:
          break;
      }

      return "";
    },
  },
  components: {
    TodoEditModal,
  },
  data() {
    return {
      editModalActive: false,
    };
  },
};
</script>

<style scoped>
.inter-400 {
  font-family: "Inter", sans-serif;
  font-optical-sizing: auto;
  font-weight: 400;
  font-style: normal;
  font-variation-settings: "slnt" 0;
}

.content {
  height: 5rem;
}

.high-priority {
  box-shadow: 0px 0px 20px hsl(348, 100%, 61%);
}
.medium-priority {
  box-shadow: 0px 0px 20px hsl(48, 100%, 67%);
}
.low-priority {
  box-shadow: 0px 0px 20px hsl(204, 86%, 53%);
}
</style>