<template>
  <div class="todoListTemplate text-center bg-light p-5 rounded">
    <h1 class="h3 mb-3 fw-normal">{{ title }}</h1>
    <TodoForm @addTodo="addTodo" />
    <TodoItemList :todos="todos" @remove="remove" @checked="checked" />
    <TodoAction
      :leftCount="leftCount"
      :viewState="viewState"
      @setViewState="setViewState"
    />
  </div>
</template>

<script>
import TodoForm from "./TodoForm.vue";
import TodoItemList from "./TodoItemList.vue";
import TodoAction from "./TodoAction.vue";

export default {
  data() {
    return {
      id: 1,
      todos: [],
      viewState: "all",
      todoStorage: [],
      todosJS: null,
      leftCount: 0,
    };
  },
  props: ["title"],
  components: {
    TodoForm,
    TodoItemList,
    TodoAction,
  },
  methods: {
    addTodo(input) {
      this.todoStorage.push({ id: this.id++, text: input, checked: false });
      this.changeTodoStorage();
    },
    remove(id) {
      this.todoStorage = this.todoStorage.filter((todo) => todo.id !== id);
      this.changeTodoStorage();
      console.log(this.todoStorage);
    },
    checked(id, checked) {
      this.todoStorage.map((todo) => {
        if (todo.id === id) todo.checked = checked;
      });
      this.changeTodoStorage();
      console.log(this.todos);
    },
    setViewState(viewState) {
      if (viewState == "clear") {
        viewState = "all";
        this.todoStorage = this.todoStorage.filter((todo) => !todo.checked);
        this.changeTodoStorage();
      }

      if (this.viewState != viewState) {
        this.viewState = viewState;
        this.changeTodosState();
      }
      this.viewState = viewState;
      this.changeTodosState();
    },
    changeTodosState() {
      console.log(this.viewState);
      if (this.viewState == "all") {
        this.todos = this.todoStorage;
      } else if (this.viewState == "uncheck") {
        this.todos = this.todoStorage.filter((obj) => {
          return !obj.checked;
        });
      } else if (this.viewState == "check") {
        this.todos = this.todoStorage.filter((obj) => {
          return obj.checked;
        });
      }
    },
    changeTodoStorage() {
      localStorage.setItem("todoStorage", JSON.stringify(this.todoStorage));
      this.changeTodosState();
      this.leftCount = this.todoStorage.filter((obj) => {
        return !obj.checked;
      }).length;
    },
  },
  created() {
    console.log("localStorage loading..");
    try {
      this.todosJS = JSON.parse(localStorage.getItem("todoStorage"));
      this.id = this.todosJS.at(-1)["id"] + 1;
      this.todoStorage = this.todosJS || [];
      this.changeTodosState();
      this.leftCount = this.todoStorage.filter((obj) => {
        return !obj.checked;
      }).length;
    } catch {
      console.log("localstorage parsing error");
    }
  },
};
</script>
