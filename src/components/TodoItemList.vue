<template>
  <div class="todoItemList list-group w-auto">
    <transition-group name="list" tag="section">
      <TodoItem
        v-for="(todo, idx) in todos"
        :todo="todo"
        @remove="remove"
        @checked="checked"
        :key="todo"
      ></TodoItem>
    </transition-group>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  props: ["todos"],
  components: {
    TodoItem,
  },
  methods: {
    checked(id, checked) {
      this.$emit("checked", id, checked);
    },
    remove(id) {
      this.$emit("remove", id);
    },
  },
};
</script>

<style>
.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-move {
  transition: transform 0.3s;
}
.list-enter-active,
.list-leave-active {
  transition: all 0.3s;
}
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
