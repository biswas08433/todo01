<template>
  <div
    class="modal"
    :class="{ 'is-active': active }"
  >
    <div
      class="modal-background"
      @click="$emit('deactivate')"
    ></div>
    <div class="modal-content">
      <ModalForm
        form-action="Add"
        @submitted="(formData) => $emit('add', formData)"
      />
    </div>
    <button
      class="modal-close is-large"
      aria-label="close"
      @click="$emit('deactivate')"
    ></button>
  </div>
</template>

<script>
  import ModalForm from '@/components/ModalForm.vue';


  export default {
    components: {
      ModalForm
    },
    props: ["active"],
    computed: {
      priorityColor: function () {
        return "is-info";
      },
    },
    data: function () {
      return {
        formTodo: {
          todoTitle: "",
          todoDescription: "",
          todoPriority: "High",
        },
      };
    },
  };
</script>
