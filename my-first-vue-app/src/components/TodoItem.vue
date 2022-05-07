<template>
  <p :class="['todo-item', todoProps.completed ? 'is-completed' : '']">
    <input type="checkbox" :checked="todoProps.completed" />
    {{ todoProps.title }}
    <button class="del-btn">Delete</button>
  </p>
</template>

<script>
import { ref } from "vue";
export default {
  name: "TodoItem",
  props: ["todoProps"],
  setup() {
    const new_id = ref("my-new-id");
    return {
      new_id,
    };
  },
};
</script>

<style scoped>
.todo-item {
  padding: 10px;
  margin: 0;
  background: #f4f4f4;
  border-bottom: 1px #ccc solid;
}
.is-completed {
  text-decoration: line-through;
}
.del-btn {
  background: #fff000;
  color: black;
  border-radius: 4px;
  cursor: pointer;
}
</style>