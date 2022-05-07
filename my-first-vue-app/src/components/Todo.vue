<template>
  <div>
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todoProps="todo"
      v-on:item-completed="markComplete"
      @deleteItem="deleteTodo"
    />
  </div>
</template>

<script>
import { ref } from "vue";

import TodoItem from "./TodoItem.vue";

export default {
  name: "TodoList",
  components: { TodoItem },
  setup() {
    const todos = ref([
      {
        id: 1,
        title: "Viec 1",
        completed: false,
      },
      {
        id: 2,
        title: "Viec 2",
        completed: false,
      },
      {
        id: 3,
        title: "Viec 3",
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
    return {
      todos,
      markComplete,
      deleteTodo,
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