<script setup>
import { ref } from 'vue';
const newTodo = ref('');

const defaultData = [{
  done: false,
  content: 'Write a blog post'
}]
const todosData = JSON.parse(localStorage.getItem('todos')) || defaultData;
const todos = ref(todosData);
function addTodo() {
  if (newTodo.value) {
    todos.value.push({
      done: false,
      content: newTodo.value
    });
    newTodo.value = '';
  }
  saveData();
}
function doneTodo(todo) {
  todo.done = !todo.done

  saveData();
}
function removeTodo(index) {
  todos.value.splice(index, 1);
  saveData();
}
function saveData() {
  const storageData = JSON.stringify(todos.value);
  localStorage.setItem('todos', storageData);
}

</script>
<template>
	<div class="bg-white rounded shadow p-6 m-4">
        <h1 class="text-grey-800 font-bold text-2xl">Todo List</h1>
        <form @submit.prevent="addTodo()" class="flex mt-4">
          <input
            v-model="newTodo"
            name="newTodo"
            autocomplete="off"
            class="border rounded w-full py-2 px-3 mr-4 text-grey-800"
            placeholder="Add Todo"
          />
          <button
            class="flex-no-shrink p-2 border-2 rounded text-teal-400 border-teal-400 hover:text-white hover:bg-teal-400"
          >Add</button>
        </form>
      </div>
      <div class="bg-white rounded shadow p-6 m-4">
        <ul>
          <li v-for="(todo, index) in todos" :key="index">
            <div class="flex mb-4 items-center">
              <p class="w-full text-grey-darkest">
                <span
                  :class="{ 'line-through': todo.done }"
                  @click="doneTodo(todo)"
                >{{ todo.content }}</span>
              </p>
              <button
                @click="removeTodo(index)"
                class="flex-no-shrink p-2 ml-2 border-2 rounded text-red-400 border-red-400 hover:text-white hover:bg-red-400"
              >Remove</button>
            </div>
          </li>
        </ul>
        <h4 v-if="todos.length === 0">Add an item above</h4>
      </div>
</template>