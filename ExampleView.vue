<template>
    <div>
      <h1>My To-Do List</h1>
  
      <input type="text" v-model="todoItem">
      <button @click="addTodo">Add Task</button>
      
      <h2>To-Do List</h2>
      <ul>
        <li v-for="todo in todoList" :key="todo.id">
          <input type="checkbox" v-model="todo.completed">
          <span :class="{ done: todo.completed }">{{ todo.task }}</span>
          <button @click="removeTodo(todo)">Remove Task</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const itemId = ref(0)
  const todoItem = ref('')
  const todoList = ref([])
  
  function addTodo() {
      todoList.value.push({
          id: itemId.value++,
          task: todoItem.value,
          completed: false
      })
      todoItem.value = ""
  }
  
  function removeTodo(todoToRemove) {
      todoList.value = todoList.value.filter((todo) => todo.id !== todoToRemove.id)
  }
  
  function toggleTodoCompletion(todo) {
      todo.completed = !todo.completed
  }
  </script>
  
  <style scoped>
  .done {
      text-decoration: line-through;
  }
  
  div {
      width: 100%;
      height: 400px;
      background-color: bisque;
  }
  </style>
  