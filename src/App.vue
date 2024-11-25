
<template>
<div class="bg- bg-opacity-50 h-screen w-screen backdrop-blur-md p-4 rounded-lg">
  <h1>Todo List</h1>
<p v-if="tasks.length === 0">No tasks</p>
<form action="" @submit.prevent="addTask">

  <input type="text" class="w-full sm:w-3/5 md:1/2 lg:1/3 px-4 py-2 mx-4 my-2 border rounded-lg  focus:outline-none" v-model="newTask" placeholder="Enter a task">
  <button>Add</button>

  <hr>
  <div :class="container" v-for="task in tasks" :key="task.id">
    <input type="checkbox"  v-model="task.completed" @click="" >
    <span :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">{{ task.title }}</span>
    
  </div>

</form>
</div>
</template>

<script setup>
import { ref } from 'vue'

const todos  =  ref([])

const newTask =  ref('')

const addTask  = () => {
  tasks.value.push( {
    title :  newTask.value,
    completed :  false,
    date : new Date()
  })
  newTask.value = ''
}

const updateStatus = (task) => {
  task.completed = !task.completed
}

//  sortTasks(){
//   return tasks.value.sort((a, b) => a.date - b.date)
// }

</script>

<style>

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

</style>