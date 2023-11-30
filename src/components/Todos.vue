<script setup lang="ts">
import type { TTodo } from "@/App.vue";
import Todo from "./Todo.vue";
type TodosProps = {
  todos: TTodo[];
  removeTodo: (td: TTodo) => void;
  updateTodo: (td: TTodo) => void;
};
const { todos, removeTodo } = defineProps<TodosProps>();
</script>

<template>
  <div v-if="todos.length > 0" class="flex flex-col gap-2 mt-6">
    <Todo
      v-for="todo in todos"
      :todo="todo"
      :key="todo.id"
      :remove-todo="removeTodo"
      :update-todo="updateTodo"
    />
  </div>
  <div v-else class="mt-6 text-center text-gray-500 text-lg">No todo</div>
</template>
