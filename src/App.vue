<template>
  <div class="columns">
    <div class="container pt-6 column is-one-third">
      <!-- ADD-TODO-FORM -->
      <TodoForm :add-todo="addTodo"></TodoForm>
    </div>
    <div class="column p-6">
      <div class="fixed-grid has-3-cols">
        <div class="grid">
          <div v-for="(card, index) in todoCards" class="cell" :key="index">
            <TodoCard
              :todo-data="card"
              :update-todo-card="updateTodoCard"
              :delete-todo-card="deleteTodoCard"
            />
            <!-- {{ card }} -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TodoForm from "@/components/TodoForm.vue";
import TodoCard from "@/components/TodoCard.vue";

export default {
  components: {
    TodoForm,
    TodoCard,
  },
  created() {
    this.getTodoCards();
  },
  data() {
    return {
      cardCounter: 0,
      editModalActive: false,

      todoCards: [],
    };
  },
  methods: {
    async getTodoCards() {
      let res = await fetch("todoCards.json");
      let data = await res.json();

      this.cardCounter = data.length;
      this.todoCards = data;
    },
    addTodo(formTodo) {
      const options = {
        year: "numeric",
        month: "long",
        day: "numeric",
        hour: "numeric",
        minute: "numeric",
      };
      const formatter = new Intl.DateTimeFormat("en-US", options);
      if (formTodo.todoTitle !== "") {
        this.todoCards.push({
          todoIndex: this.cardCounter,
          todoTitle: formTodo.todoTitle,
          todoDescription: formTodo.todoDescription,
          todoPriority: formTodo.todoPriority,
          todoCreationTime: formatter.format(Date.now()),
        });
      }
      this.cardCounter++;
    },
    deleteTodoCard(index) {
      let arrayIndex = this.todoCards.findIndex((e) => e.todoIndex === index);
      this.todoCards.splice(arrayIndex, 1);
    },
    updateTodoCard(todo) {
      let arrayIndex = this.todoCards.findIndex(
        (e) => e.todoIndex === todo.todoIndex
      );
      this.todoCards[arrayIndex] = todo;
    },
  },
};
</script>