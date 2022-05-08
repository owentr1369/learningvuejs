<template>
  <AddTodo @add-todo="addTodo" />
  <TodoItem
    v-for="todo in todos"
    :key="todo.id"
    :todoProps="todo"
    v-on:item-completed="markComplete"
    @deleteItem="deleteTodo"
  />
</template>

<script>
import { ref } from "vue";

import TodoItem from "./TodoItem.vue";
import AddTodo from "./AddTodo.vue";
import { v4 as uuidv4 } from "uuid";

export default {
  name: "TodoList",
  components: { TodoItem, AddTodo },
  setup() {
    const todos = ref([
      {
        id: uuidv4(),
        title: "Học VueJS",
        completed: false,
      },
      {
        id: uuidv4(),
        title: "Ôn JavaScript",
        completed: false,
      },
      {
        id: uuidv4(),
        title: "HTML CSS",
        completed: false,
      },
    ]);
    const markComplete = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id === id) todo.completed = !todo.completed;
        return todo;
      });
    };
    const deleteTodo = (id) => {
      todos.value = todos.value.filter((todo) => todo.id !== id);
    };
    const addTodo = (newTodo) => {
      todos.value.push(newTodo);
    };
    return {
      todos,
      markComplete,
      deleteTodo,
      addTodo,
    };
  },
};
</script>

<style scoped>
div {
  width: 60%;
  margin: 4rem auto;
  font-size: 1rem;
}
</style>