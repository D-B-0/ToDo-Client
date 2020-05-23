<template>
  <div class="todo-list">
    <div v-for="todo in todos" :key="todo._id">
      <Todo :todo="todo" :refreshApp="refreshApp" />
    </div>
    <h4 v-if="todos.length == 0">There are no todos!</h4>
    <p>
      <label for="new-todo">New todo:&nbsp;</label>
      <input
        id="new-todo"
        type="text"
        placeholder="Todo description"
        v-model="description"
        @keyup.enter="createTodo"
        required
      />
    </p>
    <p class="error" v-if="error">{{error}}</p>
  </div>
</template>

<script>
import Todo from "./Todo.vue";
export default {
  data() {
    return {
      todos: [],
      description: "",
      error: ""
    };
  },
  methods: {
    createTodo() {
      fetch("http://localhost:8080/todo", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({ description: this.description })
      })
        .then(res => res.json())
        .then(res => {
          console.log(res);
          this.error = res.error;
          this.refreshApp();
        })
        .catch(console.error);
    },
    refreshApp() {
      window.location.reload(true);
    }
  },
  created() {
    fetch(`${window.location.protocol}//${window.location.hostname}:8080/todo`)
      .then(res => res.json())
      .then(res => {
        this.todos = res.data;
      })
      .catch(console.error);
  },
  components: {
    Todo
  }
};
</script>

<style>
</style>
