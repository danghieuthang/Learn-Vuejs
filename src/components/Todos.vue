<template>
  <ul>
    <!-- v-for và v-bind lúc nào cũng đi cùng với nhau -->
    <AddTodo @add-todo="addTodo" />
    <TodoItem
      v-for="title in todos"
      v-bind:key="title.id"
      v-bind:todoProps="title"
      @mark-todo="markCompleted"
      @delete-todo="deleteTodo"
    />
  </ul>
</template>

<script>
import { ref } from "vue";
import TodoItem from "../components/TodoItem";
import AddTodo from "../components/AddTodo";
// import { v4 as uuidv4 } from "uuid";
import axios from "axios";
// npm i axios -- Thư viện javascript sử dụng để tạo ra những HTTP request tới API nào đó
export default {
  name: "Todos",
  components: { TodoItem, AddTodo },
  setup() {
    // trạng thái khởi điểm
    const todos = ref([
      //   { id: uuidv4(), title: "To do 1", completed: false },
      //   { id: uuidv4(), title: "To do 2", completed: true },
      //   { id: uuidv4(), title: "To do 3", completed: false },
    ]);
    // Hàm bất đồng bộ
    const getAllTodos = async () => {
      try {
        const result = await axios.get(
          "http://jsonplaceholder.typicode.com/todos?_limit=5"
        );
        todos.value = result.data;
        console.log(result.data);
      } catch (error) {
        console.log(error);
      }
    };

    getAllTodos();

    const markCompleted = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id === id) todo.completed = !todo.completed;
        return todo;
      });
    };

    // const deleteTodo = (id) => {
    //   todos.value = todos.value.filter((todo) => todo.id != id);
    // };

    const deleteTodo = async id => {
      try {
          await axios.delete('http://jsonplaceholder.typicode.com/todos/${id}');
          todos.value = todos.value.filter((todo) => todo.id != id);
      } catch (error) {
          console.log(error);
      }
    };

    const addTodo = (newTodo) => {
      todos.value.push(newTodo);
    };

    return {
      todos,
      markCompleted,
      deleteTodo,
      addTodo,
    };
  },
};
</script>

<style></style>
