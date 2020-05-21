<template>
  <div id="app">
    <h1>Todos</h1>
    <ListTodos />
  </div>
</template>

<script>
import ListTodos from "@/components/ListTodos.vue";
export default {
  name: "App",
  components: {
    ListTodos
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px;
  margin-bottom: 0;
  font-size: 25px;
  display: flex;
  flex-direction: column;
}

input[type="text"] {
  font-size: 1rem;
  border: none;
  background-color: rgb(219, 219, 219);
  border-radius: 0.6rem;

  &.crossed {
    text-decoration: line-through;
  }

  &:focus {
    border: 0.1rem solid rgb(0, 182, 182);
  }
}
</style>
