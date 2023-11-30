<script setup lang="ts">
import type { TTodo } from "@/App.vue";
type TodoProps = {
  todo: TTodo;
  removeTodo: (todo: TTodo) => void;
  updateTodo: (todo: TTodo) => void;
};
const props = defineProps<TodoProps>();
const baseStyle = "grow p-2 rounded-md bg-blue-100 w-full break-all";
const completedStyle = "line-through text-gray-500";
</script>
<template>
  <div class="flex items-center gap-2">
    <input
      :checked="todo.completed"
      type="checkbox"
      class="w-6 h-6"
      @change="
        updateTodo({
          ...props.todo,
          completed: !props.todo.completed,
        })
      "
    />
    <p :class="todo.completed ? baseStyle + ' ' + completedStyle : baseStyle">
      {{ props.todo.name }}
    </p>
    <button
      @click="props.removeTodo(todo)"
      class="py-2 px-4 border border-gray-100 rounded-md text-red-600"
    >
      X
    </button>
  </div>
</template>
