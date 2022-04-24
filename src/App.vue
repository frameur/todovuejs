<template>
  <h1>&#8216;market list&#8217;</h1>
  <Form @add="saveTodo" />

  <TodoList :todos="todos" @delete-todo="deleteTodo" @edit-todo="editTodo" />
</template>

<script>
import Form from "@/components/Form";
import TodoList from "@/components/TodoList";
import { ref } from "vue";
export default {
  name: "App",
  components: {
    Form,
    TodoList,
  },
  setup() {
    let todos = ref([]);
    const saveTodo = function(data) {
      console.log("App | saveTodo() | data", data);
      todos.value = [...todos.value, { todo: data, id: Date.now() }];
      console.log("App | saveTodo() | todos.value", todos.value);
    };

    const editTodo = function(tod) {
      todos.value = todos.value.map((t) => (t.id !== tod.id ? t : tod));
    };
    const deleteTodo = function(tod) {
      console.log("App | deleteTodo() | tod", tod);
      todos.value = todos.value.filter((t) => t.id !== tod.id);
    };
    return {
      saveTodo,
      deleteTodo,
      todos,
      editTodo,
    };
  },
};
</script>

<style>
body {
  background: url(./assets/listcourse.jpg) center/cover;
  height: 100vh;
  margin: 0;
  padding: 0;
  overflow-x: hidden;
}

h1 {
  text-transform: uppercase;
  text-shadow: 4px 4px 2px rgba(41, 38, 38, 0.6);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #e1e5e9;
  margin-top: 60px;
}
</style>
