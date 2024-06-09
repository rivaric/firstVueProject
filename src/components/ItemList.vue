<script>
import Item from "./Item.vue";
import { defineComponent } from "vue";

export default defineComponent({
  components: {
    Item,
  },
  props: {
    todos: {
      type: Array,
      required: true,
    },
    changeStatus: {
      type: Function,
      required: true,
    },
    deleteTodo: {
      type: Function,
      required: true,
    },
  },
});
</script>

<template>
  <div v-if="todos.length > 0" v-for="todo in todos" class="todos">
    <Item
      :todo="todo"
      @change-status="changeStatus"
      @delete-todo="deleteTodo"
    />
  </div>
  <div v-else>
    <p style="text-align: center">Нет задач</p>
  </div>
</template>

<style scoped>
.todos {
  display: flex;
  flex-direction: column;
}
</style>
