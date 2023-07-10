<template>
  <span>
    <input type="text" v-model="newTodo" placeholder="할 일 입력" />
    <input type="submit" @click.prevent="addTodo" />
  </span>

  <ul>
    <li v-for="(todo, index) in todos">
      <span :class="{ completed: todo.state }">{{ todo.text }}</span>
      <button @click="toggleTodoStatus(index)">
        {{ todo.state ? "완료" : "미완료" }}
      </button>
      <button @click="removeTodo(index)">삭제</button>
    </li>
  </ul>
</template>

<script>
import { reactive, ref } from "vue";

export default {
  setup() {
    const todos = reactive([
      { id: Date.now(), text: "Vue 배우기", state: true },
      { id: Date.now(), text: "Vue 프로젝트", state: false },
      { id: Date.now(), text: "Vue 공부", state: false },
    ]);

    const newTodo = ref("");

    const addTodo = () => {
      if (newTodo.value.trim() == "") return;
      todos.push({ id: Date.now(), text: newTodo.value, state: false });
      newTodo.value = "";
    };

    const toggleTodoStatus = (index) => {
      todos[index].state = !todos[index].state;
    };

    const removeTodo = (index) => {
      todos.splice(index, 1);
    };

    return {
      todos,
      newTodo,
      addTodo,
      toggleTodoStatus,
      removeTodo,
    };
  },
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
