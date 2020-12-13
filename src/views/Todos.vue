<template>
  <div>
    <Addtodo v-on:add-todo="addTodo" />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="uncompleted">Uncompleted</option>
    </select>
    <Loader v-if="loading" />
    <Todos
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @del-todo="delTodo"
    />
    <p v-else>Todos not found</p>
  </div>
</template>

<script>
import Todos from "@/components/Todos";
import Addtodo from "@/components/Addtodo";
import Loader from "@/components/Loader";
import axios from "axios";

export default {
  name: "App",
  components: {
    Todos,
    Addtodo,
    Loader,
  },
  data() {
    return {
      todos: [],
      loading: true,
      filter: "all",
    };
  },
  // mounted() {
  //   fetch("https://jsonplaceholder.typicode.com/todos?_limit=5")
  //     .then((response) => response.json())
  //     .then((json) => {
  //       setTimeout(() => {
  //         this.todos = json;
  //       }, 500);
  //     });
  // },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((res) => {
        setTimeout(() => {
          this.todos = res.data;
          this.loading = false;
        }, 1000);
      })
      .catch((err) => console.log(err));
  },
  computed: {
    filteredTodos() {
      let data = {};
      switch (this.filter) {
        case "all":
          data = this.todos;
          break;
        case "completed":
          data = this.todos.filter((item) => item.completed);
          break;
        case "uncompleted":
          data = this.todos.filter((item) => !item.completed);
          break;
        default:
          false;
          break;
      }
      return data;
    },
  },
  methods: {
    delTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then((this.todos = this.todos.filter((todo) => todo.id !== id)))
        .catch((err) => console.log(err));
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed,
        })
        .then((res) => (this.todos = [...this.todos, res.data]))
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
select {
  width: 150px;
  text-align-last: right;
  padding-right: 29px;
  direction: rtl;
}
</style>
