<template>
  <p
    :class="['todo-item', todoProps.completed ? 'is-completed' : '']"
    :id="itemId"
  >
    <input type="checkbox" :checked="todoProps.completed" @change="markTodo" />
    {{ todoProps.title }}
    <button class="del-btn" @click="deleteTodo">Delete</button>
  </p>
  <!-- <li>{{ todoProps.todo }}</li> -->
</template>

<script>
import { ref } from "vue";
export default {
  name: "TodoItem",
  props: ["todoProps"],
  setup(props, context) {
    const itemId = ref("");
    const markTodo = () => {
      const id = props.todoProps.id;
      context.emit("mark-todo", id);
    };
    const deleteTodo = () => {
      const id = props.todoProps.id;
      context.emit("delete-todo", id);
    };
    return { itemId, markTodo, deleteTodo };
  },
};
</script>

<style>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  margin: 0;
  border-bottom: 1px #ccc dotted;
}
.del-btn {
  background: #ff0000;
  color: #fff;
  border: none;
  cursor: pointer;
  float: right;
}
.is-completed {
  text-decoration: line-through;
}
</style>
