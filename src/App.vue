<template>
  <div>
    <h1>TodoList</h1>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo" placeholder="Add New Todo">
      <button>Add Todo</button>
    </form>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" v-model="todo.completed">
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <span v-if="todo.created" class="created-time">{{ todo.created.toLocaleString() }}</span>
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
      const newTodoObj = {
        text: newTodo.value,
        completed: false,
        created: new Date(),
      };
      if (newTodoObj.text === '') {
        return;
      }
      todos.value.push(newTodoObj);
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

.created-time {
  font-size: 12px;
  margin-left: 10px;
  color: gray;
}

h1 {
  text-align: center;
}
</style>
