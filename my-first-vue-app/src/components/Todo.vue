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
import axios from "axios";
import TodoItem from "./TodoItem.vue";
import AddTodo from "./AddTodo.vue";

export default {
  name: "TodoList",
  components: { TodoItem, AddTodo },
  setup() {
    const todos = ref([]);
    const getAllTodos = async () => {
      try {
        const res = await axios.get(
          "https://jsonplaceholder.typicode.com/todos?_limit=10"
        );
        todos.value = res.data;
      } catch (error) {
        console.log(error);
      }
    };
    getAllTodos();
    const markComplete = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id === id) todo.completed = !todo.completed;
        return todo;
      });
    };
    const deleteTodo = async (id) => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
        todos.value = todos.value.filter((todo) => todo.id !== id);
      } catch (error) {
        console.log(error);
      }
    };
    const addTodo = async (newTodo) => {
      try {
        const res = await axios.post(
          `https://jsonplaceholder.typicode.com/todos/`,
          newTodo
        );
        todos.value.push(res.data);
      } catch (error) {
        console.log(error);
      }
      // todos.value.push(newTodo);
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