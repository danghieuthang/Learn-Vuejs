<template>
  <form action="" @submit="addItem">
    <input type="text" placeholder="Add new work" v-model="title" />
    <input value="Add" type="submit" class="btn-add" />
  </form>
</template>

<script>
import { ref } from "vue";
// Thư viện tự động tạo id
import { v4 as uuidv4 } from "uuid";
export default {
  name: "Addtitle",
  setup(props, context) {
    const title = ref("");
    const addItem = (event) => {
      // Ngăn chuyển đến action
      event.preventDefault();

      const newItem = {
        id: uuidv4(),
        title: title.value,
        completed: false,
      };

      //gọi hàm add-todo trong thàng gọi nó với tham số là newItem
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
input[type="submit"] {
  flex: 2;
  padding: 5px;
}
</style>
