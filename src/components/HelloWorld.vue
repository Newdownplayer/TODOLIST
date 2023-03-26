<template>
  <div>
    <h1>Vue3 TodoList</h1>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo" placeholder="Add New Todo">
      <button>Add Todo</button>
    </form>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" v-model="todo.completed">
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <button @click="removeTodo(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTodo = ref('');
    const todos = ref([
      { text: 'Learn Vue', completed: false },
      { text: 'Build a Vue app', completed: false },
    ]);

    function addTodo() {
      todos.value.push({ text: newTodo.value, completed: false });
      newTodo.value = '';
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    return {
      newTodo,
      todos,
      addTodo,
      removeTodo,
    };
  },
};
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>
