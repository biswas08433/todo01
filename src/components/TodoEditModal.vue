<template>
  <div class="modal" :class="{ 'is-active': active }">
    <div class="modal-background" @click="$emit('deactivate')"></div>
    <div class="modal-content">
      <ModalForm
        :filler-data="filler"
        form-action="Update"
        @submitted="(formData, index) => $emit('update', formData, index)"
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
import ModalForm from "@/components/ModalForm.vue";

export default {
  props: ["filler", "active"],
  components: {
    ModalForm,
  },
};
</script>
