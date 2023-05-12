<template>
  <div id="app">
    <TodoListFrame :title="title"></TodoListFrame>
  </div>
</template>

<script>
import TodoListFrame from "./components/TodoListFrame.vue";
export default {
  data() {
    return {
      title: "Todo",
    };
  },
  components: {
    TodoListFrame: TodoListFrame,
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
  background: #f9f9f9;
}
</style>
