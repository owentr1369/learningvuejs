<template>
  <p :class="['todo-item', todoProps.completed ? 'is-completed' : '']">
    <input
      type="checkbox"
      :checked="todoProps.completed"
      @change="markItemCompleted"
    />
    {{ todoProps.title }}
    <button class="del-btn" @click="deleteItem">Delete</button>
  </p>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todoProps"],
  setup(props, context) {
    const markItemCompleted = () => {
      context.emit("item-completed", props.todoProps.id);
    };
    const deleteItem = () => {
      context.emit("delete-item", props.todoProps.id);
    };
    return {
      markItemCompleted,
      deleteItem,
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