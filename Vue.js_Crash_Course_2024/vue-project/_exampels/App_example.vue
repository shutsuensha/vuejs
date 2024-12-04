<script setup>
import { onMounted, ref } from 'vue'

const name = ref('Danya')
const status = ref('active')
const tasks = ref(null)
const newTask = ref('')

function toggleStatus() {
  if (status.value === 'active') {
    status.value = 'pending'
  } else if (status.value === 'pending') {
    status.value = 'inactive'
  } else {
    status.value = 'active'
  }
}

function addTask() {
  tasks.value.push(newTask.value)
  newTask.value = ''
}

function deleteTask(task) {
  tasks.value = tasks.value.filter((el) => el != task)
}


onMounted(async () => {
  try {
    const resposne = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await resposne.json()
    tasks.value = data.map((el) => el.title)
  } catch (error) {
    console.log(`Error fetching: ${error}`)
  }
})
</script>

<template>
  <h1>{{ name }}</h1>

  <br />
  
  <p v-if="status ==='active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <br />

  <form @submit.prevent="addTask">
    <input v-model="newTask" required placeholder="new task">
    <button>Add Task</button>
  </form>

  <br />

  <ul>
    <li v-for="task in tasks" :key="task"> 
      <snap>
        {{ task }}
      </snap>
      <button @click="deleteTask(task)">X</button>
    </li>
  </ul>

  <br />

  <button @click="toggleStatus">change status</button>
</template>