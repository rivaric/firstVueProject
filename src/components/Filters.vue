<template>
  <div class="filters">
    <input placeholder="Поиск задачи" class="input-search" @input="onSearch" />
    <div class="filters__tabs" v-for="{ label, value } in tabs">
      <Button :text="label" @click="onTabClick(value)" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Button from "./Button.vue";

export default defineComponent({
  components: { Button },
  emits: ["search", "tab-click"],
  data() {
    return {
      tabs: [
        { label: "Все", value: null },
        {
          label: "Выполненные",
          value: true,
        },
        {
          label: "Невыполненные",
          value: false,
        },
      ],
    };
  },
  methods: {
    onSearch(event: any) {
      this.$emit("search", event.target.value);
    },
    onTabClick(tab: boolean | null) {
      this.$emit("tab-click", tab);
    },
  },
});
</script>

<style scoped>
.filters {
  margin-bottom: 20px;
}

.input-search {
  width: 100%;
  margin-bottom: 5px;
}

.filters__tabs {
  display: flex;
  justify-content: space-between;
}
</style>
