<script setup lang="ts">
import type { TTodo } from "@/App.vue";
import { ref } from "vue";

const props = defineProps<{
  addTodo: (todo: TTodo) => void;
  total: number;
}>();

const name = ref("");
const add = () => {
  if (name.value.trim() === "") return;
  props.addTodo({
    id: props.total + 1,
    name: name.value,
    completed: false,
  });
  name.value = "";
};
</script>
<template>
  <div class="flex gap-1">
    <input
      v-model="name"
      type="text"
      class="grow bg-gray-100 rounded-md p-2 outline-0"
      placeholder="Plan something..."
      @keydown.enter="add"
    />
    <button
      class="px-4 text-gray-600 py-2 border border-gray-100 rounded-md"
      @click="add"
    >
      Add
    </button>
  </div>
</template>
