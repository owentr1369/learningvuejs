<template>
  <div id="app">
    <p>VueJS Learning</p>
    <HeaderApp />
    <TodoList />
  </div>
</template>

<script>
import HeaderApp from "./components/HeaderApp.vue";
import TodoList from "./components/Todo.vue";
export default {
  name: "App",
  components: { HeaderApp, TodoList },
};
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 2rem;
  font-weight: 700;
  text-align: center;
}
</style>