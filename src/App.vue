<script setup>
import { ref } from 'vue';
import TaskComponent from './components/TaskComponent.vue';

let tasks = ref([])
let warning = ref('')
let currentDate = ref('')
let message = ''
let date = ''

const addTask = () => {

  if (message.length > 0 && date.length > 0) {
    const newTask = {
      message: message,
      date: date,
    }

    warning.value = ''
    tasks.value.push(newTask)
  } else {
    warning.value = 'Complete los campos'
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}

const deleteAll = () => {
  tasks.value = []
}

const updateDateTime = () => {
  var today = new Date()
  var now = today.toLocaleString()
  currentDate.value = now
}

updateDateTime()
setInterval(updateDateTime, 1000)

</script>

<template>
  <div class="text-center mt-6">
    <div class="inline-block w-[300px] bg-[#f1f1f1] p-4 rounded">
      <p class=" px-3 text-lg font-bold font-mono bg-slate-400 rounded">TASKS</p>

      <label>Task: </label>
      <input class="mt-2 text-center border-[#f1f1f1] shadow rounded" v-model="message" type="text"
        placeholder="Ingrese tarea">
      <label>Deadline: </label>
      <input class="w-[150px] mt-1 text-center border-[#f1f1f1] shadow rounded" v-model="date" type="time"
        placeholder="Ingrese fecha limite">

      <button class="bg-slate-400 cursor-pointer hover:bg-slate-500 rounded-lg mt-4 px-6 float-left"
        @click="addTask">ADD</button>
      <button v-show="tasks.length > 0"
        class="float-right bg-slate-400 cursor-pointer hover:bg-slate-500 rounded-lg mt-4 px-6 ml-2" @click="deleteAll">
        DELETE ALL</button>

      <div class="mt-3">
        {{ warning }}
      </div>
    </div>
  </div>

  <div v-show="tasks.length > 0" class="ml-[22%] mt-4 font-medium shadow rounded-t-lg inline-block px-2">
    Date: {{ currentDate }}
  </div>

  <div v-show="tasks.length > 0" class="mt-4 font-medium shadow rounded-t-lg inline-block px-2 mr-[22%] float-right">
    N° de tareas: {{ tasks.length }}
  </div>

  <div v-show="tasks.length > 0" class="border-2 shadow rounded-lg mt-1 p-3 mx-[20%]">
    <div class="text-center">
      <TaskComponent v-for="(task, index) in tasks" :key="index" :message="task.message" :date="task.date" :index="index"
        @deleteTask="deleteTask" />
    </div>
  </div>
</template>

<style scoped></style>