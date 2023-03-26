<template>
  <div>
    <h1>TodoList</h1>
    <form @submit.prevent="addTodo">
      <input type="text" v-model="newTodo" placeholder="Add New Todo" class="input">
      <button>Add Todo</button>
    </form>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <div class="list">
          <div>
            <input type="checkbox" v-model="todo.completed">
            <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
          </div>
          <span v-if="todo.created" class="created-time">{{ todo.created.toLocaleString() }}</span>
          <button @click="removeTodo(index)">Delete</button>
        </div>
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

li {
  list-style: none;
}

li button {
  color: rgb(201, 147, 147);
  background-color: white;
  border: 1px solid rgb(163, 116, 116);
  border-radius: 4px;
}


h1 {
  text-align: center;
  margin: 32px;
}


form {
  display: flex;
  justify-content: center;
  margin-bottom: 32px;
}

.input {
  margin-right: 10px;
}

.list {
  margin: 12px;
  text-align: center;
  display: flex;
  justify-content: space-between;
}
</style>
