<script>
import TodoItem from "./components/TodoItem.vue";

export default {
  components: {
    TodoItem,
  },
  data() {
    return {
      todoList: null,
      newTodo: "",
    };
  },
  methods: {
    getTodoList() {
      return localStorage.getItem("todoList").split("///");
    },
    add() {
      if (this.newTodo) {
        this.todoList.push(this.newTodo);
        localStorage.setItem("todoList", this.todoList.join("///"));
        this.newTodo = "";
      }
    },
    update(index, value) {
      this.todoList[index] = value;
      localStorage.setItem("todoList", this.todoList.join("///"));
    },
    destroy(index) {
      this.todoList.splice(index, 1);
      localStorage.setItem("todoList", this.todoList.join("///"));
    },
  },
  mounted() {
    this.todoList = this.getTodoList();
  },
};
</script>

<template>
  <main>
    <div class="header">Todo List</div>
    <div>
      <TodoItem
        v-for="(todo, index) in todoList"
        :key="index"
        :todo="todo"
        :index="index"
        @update="update"
        @destroy="destroy"
      />
    </div>
    <div>
      <input v-model="newTodo" type="text" placeholder="Add something..." />
      <button @click="add">Add</button>
    </div>
  </main>
</template>

<style scoped>
main {
  width: 400px;
  height: 500px;
  margin: auto;
  padding: 10px;
  border-radius: 0.25rem;
  background-color: white;
  box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
}
</style>
