<template>
  <Navbar @add="() => (addModalData.active = true)" />
  <div class="columns">
    <!-- <div class="container pt-6 column is-one-third">
      <TodoForm :add-todo="addTodo" />
    </div> -->
    <div class="column p-6">
      <div class="fixed-grid has-4-cols">
        <div class="grid">
          <TodoCard
            v-for="(card, index) in todoCards"
            :key="index"
            :todo-data="card"
            @edit-request="showEditModal(index)"
            @delete-request="deleteTodoCard(index)"
          />
          <!-- {{ card }} -->
        </div>
      </div>
    </div>
  </div>
  <TodoAddModal
    :active="addModalData.active"
    @deactivate="() => (addModalData.active = false)"
    @add="(formTodo) => addTodoCard(formTodo)"
  />
  <TodoEditModal
    v-if="todoCards.length !== 0"
    :filler="todoCards[editModalData.editIndex]"
    :active="editModalData.active"
    @deactivate="() => (editModalData.active = false)"
    @update="(formTodo, index) => updateTodoCard(index, formTodo)"
  />
</template>

<script>
import TodoCard from "@/components/TodoCard.vue";
import TodoEditModal from "@/components/TodoEditModal.vue";
import TodoAddModal from "@/components/TodoAddModal.vue";
import Navbar from "@/components/Navbar.vue";

export default {
  components: {
    TodoCard,
    TodoEditModal,
    TodoAddModal,
    Navbar,
  },

  created() {
    this.getTodoCards();
  },

  data() {
    return {
      cardCounter: 0,
      editModalData: {
        active: false,
        editIndex: 0,
      },
      addModalData: {
        active: false,
      },
      todoCards: [],
    };
  },

  methods: {
    getTodoCards() {
      let res = localStorage.getItem("todos");
      let data = JSON.parse(res);

      this.cardCounter = data.length;
      this.todoCards = data;
    },

    addTodoCard(formTodo) {
      // console.log(formTodo);
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
      this.addModalData.active = false;
      localStorage.setItem("todos", JSON.stringify(this.todoCards));
    },

    updateTodoCard(index, formTodo) {
      this.editModalData.active = false;
      let arrayIndex = this.todoCards.findIndex((e) => e.todoIndex === index);
      this.todoCards[arrayIndex].todoTitle = formTodo.todoTitle;
      this.todoCards[arrayIndex].todoDescription = formTodo.todoDescription;
      this.todoCards[arrayIndex].todoPriority = formTodo.todoPriority;

      localStorage.setItem("todos", JSON.stringify(this.todoCards));
    },

    deleteTodoCard(index) {
      console.log(index);
      let arrayIndex = this.todoCards.findIndex((e) => e.todoIndex === index);
      this.todoCards.splice(arrayIndex, 1);
      localStorage.setItem("todos", JSON.stringify(this.todoCards));
    },

    showEditModal(index) {
      console.log(index);
      this.editModalData = {
        active: true,
        editIndex: index,
      };
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Fira+Sans:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Inter:wght@100..900&display=swap");

.fira-sans-regular {
  font-family: "Fira Sans", sans-serif;
  font-weight: 400;
  font-style: normal;
}
</style>