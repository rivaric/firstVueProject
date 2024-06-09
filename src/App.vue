<script lang="ts">
import ItemList from "./components/ItemList.vue";
import { defineComponent } from "vue";
import Filters from "./components/Filters.vue";
import AddItem from "./components/AddItem.vue";

interface Todo {
  id: number;
  name: string;
  done: boolean;
}

export default defineComponent({
  components: {
    ItemList,
    Filters,
    AddItem,
  },
  data() {
    return {
      todos: [] as Todo[],
      searchValue: "",
      tabValue: null as boolean | null,
    };
  },
  computed: {
    filteredTodo(): Todo[] {
      let filteredTodo = this.todos;

      if (this.searchValue) {
        filteredTodo = filteredTodo.filter((todo) =>
          todo.name.toLowerCase().includes(this.searchValue.toLowerCase())
        );
      }

      if (this.tabValue !== null) {
        filteredTodo = filteredTodo.filter(
          (todo) => todo.done === this.tabValue
        );
      }

      return filteredTodo;
    },
  },
  methods: {
    addItem(item: Todo) {
      this.todos.push(item);
    },
    changeStatus(id: number, status: boolean) {
      const updateTodoStatus = (todo: Todo) =>
        todo.id === id ? { ...todo, done: status } : todo;

      this.todos = this.todos.map(updateTodoStatus);
    },
    searchTodoByName(name: string) {
      this.searchValue = name;
    },
    changeTab(tabValue: boolean | null) {
      console.log(tabValue);

      this.tabValue = tabValue;
    },
    deleteTodo(id: number) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
  },
});
</script>

<template>
  <div>
    <AddItem @add-item="addItem" />
    <Filters @search="searchTodoByName" @tab-click="changeTab" />
    <ItemList
      :todos="filteredTodo"
      :changeStatus="changeStatus"
      :deleteTodo="deleteTodo"
    />
  </div>
</template>
