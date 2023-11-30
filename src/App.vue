<script setup lang="ts">
import { computed, ref } from "vue";
import TodoInput from "./components/TodoInput.vue";
import Todos from "./components/Todos.vue";
type Filter = "all" | "completed" | "not completed";
export type TTodo = {
  id: number;
  name: string;
  completed: boolean;
};
const todos = ref<TTodo[]>([]);
const activeTab = ref<Filter>("all");

const addTodo = (todo: TTodo) => {
  activeTab.value = "all";
  todos.value.push(todo);
};
const removeTodo = (todo: TTodo) => {
  todos.value = todos.value.filter((td) => td.id !== todo.id);
};
const updateTodo = (todo: TTodo) => {
  const index = todos.value.findIndex((td) => td.id === todo.id);
  const newTodos = todos.value;
  newTodos[index] = todo;
  todos.value = newTodos;
};
const filteredTodos = computed(() => {
  if (activeTab.value === "all") {
    return todos.value;
  }

  if (activeTab.value === "completed") {
    return todos.value.filter((todo) => todo.completed);
  }

  if (activeTab.value === "not completed") {
    return todos.value.filter((todo) => !todo.completed);
  }
});
const filters = ["All", "Completed", "Not Completed"];
const filter = (tab: Filter) => {
  activeTab.value = tab;
};
const tabBasicStyle =
  "p-2 border-b border-gray-100 cursor-pointer text-gray-600";
const tabInactiveStyle = "bg-white";
const tabActiveStyle = "bg-blue-100";
</script>

<template>
  <main class="h-[100vh]">
    <div class="py-6 h-full border border-red-500 flex justify-center">
      <div class="flex w-[60vw] shadow-md">
        <div class="h-full border border-gray-100">
          <div
            v-for="flt in filters"
            :class="
              flt.toLowerCase() === activeTab
                ? tabBasicStyle + ' ' + tabActiveStyle
                : tabBasicStyle + ' ' + tabInactiveStyle
            "
            @click="filter(flt.toLowerCase() as Filter)"
          >
            {{ flt }}
          </div>
        </div>
        <div class="p-6 grow border border-gray-100">
          <TodoInput :add-todo="addTodo" :total="todos.length" />
          <Todos
            :todos="filteredTodos ?? []"
            :remove-todo="removeTodo"
            :update-todo="updateTodo"
          />
        </div>
      </div>
    </div>
  </main>
</template>
