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
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  -ms-box-sizing: border-box;
  box-sizing: border-box;
}

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
  height: 100%;
  padding: 0.25rem;

  &.crossed {
    text-decoration: line-through;
  }

  &:focus {
    box-shadow: inset 0 0 0 0.15rem rgb(0, 182, 182);
  }
}
</style>
