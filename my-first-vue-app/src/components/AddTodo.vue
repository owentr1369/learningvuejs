<template>
  <form @submit="addItem">
    <input type="text" placeholder="Thêm việc mới..." v-model="title" />
    <input type="submit" value="Thêm" class="add-btn" />
  </form>
</template>

<script>
import { ref } from "vue";

export default {
  name: "AddTodo",
  setup(props, context) {
    const title = ref("");
    const addItem = (event) => {
      event.preventDefault();
      const newItem = {
        title: title.value,
        completed: false,
      };
      context.emit("add-todo", newItem);
      title.value = "";
    };

    return {
      title,
      addItem,
    };
  },
};
</script>

<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 10;
  padding: 5px;
}
input[type="submid"] {
  flex: 2;
}
</style>