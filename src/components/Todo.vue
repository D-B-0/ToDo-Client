<template>
  <div class="todo">
    <input type="checkbox" :disabled="loading" v-model="todo.completed" />
    <input
      type="text"
      :disabled="loading"
      v-model="tempDescription"
      @keyup.enter="updateDescription"
      :class="[todo.completed? 'crossed': '']"
    />
    <button class="x" @click="deleteTodo">X</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: false,
      tempDescription: this.todo.description
    };
  },
  props: {
    todo: Object,
    refreshApp: Function
  },
  methods: {
    updateDescription() {
      this.todo.description = this.tempDescription;
    },
    deleteTodo() {
      this.loading = true;
      fetch(this.todo.link, { method: "DELETE" }).then(res => {
        this.loading = false;
        this.refreshApp();
      });
    }
  },
  watch: {
    todo: {
      deep: true,
      handler(newTodo) {
        const newData = {
          description: newTodo.description,
          completed: newTodo.completed
        };
        this.loading = true;
        fetch(this.todo.link, {
          method: "PATCH",
          body: JSON.stringify(newData),
          headers: {
            "Content-Type": "application/json"
          }
        })
          .then(res => {
            this.loading = false;
            return res.json();
          })
          .then(res => {
            console.log(res);
          });
      }
    }
  }
};
</script>

<style scoped lang="scss">
div {
  width: 100%;
  display: flex;
  margin: 0.5rem 0;
  justify-content: center;

  * {
    margin-right: 0.5rem;
  }
}

input[type="text"] {
  width: 70%;

  &.crossed {
    text-decoration: line-through;
    filter: brightness(0.75);
  }
}

button.x {
  $size: 1.7rem;
  outline: none;
  border: none;
  border-radius: 50%;
  background-color: rgb(168, 0, 0);
  color: white;
  display: inline-flex;
  width: $size;
  height: $size;
  font-size: 2 * $size/3;
  align-items: center;
  justify-content: center;
  text-decoration: none;
  cursor: pointer;

  &:hover {
    text-decoration: underline;
  }
}
</style>
