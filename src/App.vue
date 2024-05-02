<template>
  <div>
    <Header />
    <ToDoList :todo="todo" :category="category" :toDos="toDos" @toDoDeleted="handleToDoDeleted" @toDoChecked="handleCheckedToDo"/>
    <AddToDo @toDoSubmitted="handleToDoSubmitted" />
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import ToDoList from './components/ToDoList.vue';
import AddToDo from './components/AddToDo.vue';

import { ref, onMounted } from 'vue';

const toDos = ref ([]);
const todo = '';
const category = '';
const done = false;


onMounted(() => {
  const savedToDos = JSON.parse(localStorage.getItem('toDos'));

  if (savedToDos) {
    toDos.value = savedToDos;
  }
})

const handleToDoSubmitted = (todoData) => {
  toDos.value.push({
    id: generateUniqueId(),
    todo: todoData.todo,
    category: todoData.category,
    done: false
  });

  saveToDoToLocalStorage();

};

const generateUniqueId = (id) => {
  return Math.floor(Math.random() * 1000000);
};

const handleToDoDeleted = (id) => {
  toDos.value = toDos.value.filter((todo) => todo.id !== id);
  saveToDoToLocalStorage();
};

const handleCheckedToDo = (id) => {
  const todoIndex = toDos.value.findIndex(todo => todo.id === id);
  if (todoIndex !== -1) {
    toDos.value[todoIndex].done = !toDos.value[todoIndex].done;
    saveToDoToLocalStorage();
  }
} 

const saveToDoToLocalStorage = () => {
  localStorage.setItem('toDos', JSON.stringify(toDos.value));
};

</script>