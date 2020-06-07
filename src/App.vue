<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader";
import TodoList from "./components/TodoList";
import TodoInput from "./components/TodoInput";
import TodoFooter from "./components/TodoFooter";

export default {
  name: 'app',
  components: {
    'TodoHeader': TodoHeader,
    'TodoList': TodoList,
    'TodoInput': TodoInput,
    'TodoFooter': TodoFooter,
  },
  data () {
    return {
      todoItems: [],
    }
  },
  created() {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        let items = localStorage.key(i);
        this.todoItems.push(items);
      }
    }
  },
  methods: {
    addTodo(todoItems) {
      localStorage.setItem(todoItems, todoItems);
      this.todoItems.push(todoItems);
    },
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    },
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    }
  },
}
</script>

<style>
  body {
    text-align: center;
    background-color: #F6F6F8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>
