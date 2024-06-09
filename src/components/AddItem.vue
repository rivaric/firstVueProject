<template>
  <div class="add-button">
    <label>
      Задача
      <input
        type="text"
        placeholder="Введите название"
        v-model="name"
        @keyup.enter="addItem"
      />
    </label>
    <Button text="Добавить" @click="addItem" />
  </div>
</template>

<script>
import Button from "./Button.vue";
import { defineComponent } from "vue";

export default defineComponent({
  components: {
    Button,
  },
  emits: ["add-item"],
  data() {
    return {
      name: "",
    };
  },
  methods: {
    addItem() {
      const item = {
        id: Date.now(),
        name: this.name,
        done: false,
      };

      this.$emit("add-item", item);
      this.name = "";
    },
  },
});
</script>

<style scoped>
.add-button {
  margin-bottom: 20px;
}
</style>
