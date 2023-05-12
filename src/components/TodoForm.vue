<template>
  <div class="todoForm input-group mb-1">
    <input
      type="text"
      class="form-control"
      placeholder="Input Todo"
      v-model="inputForm"
      @keyup.enter="addTodo"
    />
    <button
      type="button"
      class="createButton btn btn-outline-primary"
      @click="addTodo"
    >
      Adds
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputForm: "",
    };
  },
  methods: {
    addTodo() {
      if (this.inputForm) {
        this.$emit("addTodo", this.inputForm);
        this.inputForm = "";
      }
    },
  },
};
</script>

<style>
</style>
