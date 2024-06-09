<template>
  <div class="todo">
    <div>{{ todo.id }}</div>
    <div>{{ todo.name }}</div>
    <div v-if="!todo.done">Не выполнена</div>
    <div v-else>Выполнена</div>
    <button @click="changeStatus">Изменить статус</button>
    <button @click="deleteTodo">Удалить</button>
  </div>
</template>
<script>
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  emits: ["change-status", "delete-todo"],
  methods: {
    changeStatus() {
      this.$emit("change-status", this.todo.id, !this.todo.done);
    },
    deleteTodo() {
      this.$emit("delete-todo", this.todo.id);
    },
  },
});
</script>

<style scoped>
.todo {
  display: flex;
  justify-content: space-between;
}
</style>
