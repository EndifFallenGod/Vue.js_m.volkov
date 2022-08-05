<template>
  <div id="app">
    <h1>{{ message }}</h1>
    <h2 class="text-center">Please add new task</h2>
    <form action="" class="input-wrapper">
      <input type="text" class="p-1 mb-0" v-model.trim="inputText" />
      <button
        type="button"
        class="btn btn-outline-dark"
        :disabled="!isButtonEnabled"
        @click="addItem(inputText)"
      >
        Add
      </button>
    </form>
    <template v-if="hide1">
      <form action="" class="input-wrapper">
        <h2 class="p-1 m-0">Search</h2>
        <input type="search" class="" v-model="searchText" />
      </form>
      <select class="mb-4" v-model="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not completed</option>
      </select>
      <AppStatistics v-bind:items="todoItems"></AppStatistics>
    </template>
    <TodoList v-bind:list="filterList" @removeTodo="removeTodo"></TodoList>
  </div>
</template>

<script>
import AppStatistics from "./components/AppStatistics.vue";
import TodoList from "./components/TodolLst.vue";

export default {
  name: "App",
  data() {
    return {
      message: "Hello from Vue App",
      inputText: "",
      searchText: "",
      filter: "all",
      todoItems: [
        // { id: 1, text: "Бахнуть балтики", done: false },
        // { id: 2, text: "task2", done: false },
        // { id: 3, text: "Поспорить о США", done: true },
        // { id: 4, text: "task4", done: false },
        // { id: 5, text: "task 5", done: false },
      ],
    };
  },
  components: {
    AppStatistics,
    TodoList,
  },
  computed: {
    isButtonEnabled() {
      return this.inputText !== "";
    },

    filterList() {
      let list = this.todoItems.filter(
        (elem) => elem.text.toLowerCase().indexOf(this.searchText) > -1
      );
      if (this.filter === "all") {
        return list;
      }
      if (this.filter === "completed") {
        return list.filter((value) => value.done);
      } else {
        return list.filter((value) => !value.done);
      }
    },
    hide1() {
      return this.todoItems.length > 0;
    },
  },

  async mounted() {
    const data = await localStorage.getItem("todoItems");
    if (data) {
      this.todoItems = JSON.parse(data);
    }
  },

  methods: {
    addItem(name) {
      this.todoItems.push({
        id: this.todoItems.length + 1,
        text: name,
        done: false,
      });
      localStorage.setItem("todoItems", JSON.stringify(this.todoItems));
      this.inputText = "";
    },
    removeTodo(index) {
      this.todoItems.splice(index, 1);
      localStorage.setItem("todoItems", JSON.stringify(this.todoItems));
    },
  },
};
</script>

<!-- <style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style> -->
