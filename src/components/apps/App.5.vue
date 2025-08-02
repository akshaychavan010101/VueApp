<template>
  <h1>hellow {{ name }}</h1>
  <p v-if="status == 'active'">active</p>
  <p v-else-if="status == 'pending'">not</p>
  <p v-else-if="status == 'inactive'">yup</p>
  <p v-else>no</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" name="task" id="name" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <h2>Tasks:</h2>
  <ul>
    <li v-for="(task, index) in tasks">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>
  <button @click="toggle">Change</button>
</template>
<script setup>
import { onMounted, ref } from "vue";

const name = ref("jobh");
const newTask = ref("");
const status = ref("active");
const tasks = ref([1, 2, 3]);
const toggle = () => {
  if (status.value == "active") {
    status.value = "pending";
  } else if (status.value == "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};
const addTask = () => {
  if (newTask.value.trim()) tasks.value.push(newTask.value);
  newTask.value = "";
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await res.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log("Error", error);
  }
});
</script>
