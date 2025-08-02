<template>
  <h1>hellow {{ name }}</h1>
  <p v-if="status == 'active'">active</p>
  <p v-else-if="status == 'pending'">not</p>
  <p v-else-if="status == 'inactive'">yup</p>
  <p v-else>no</p>
  <ul>
    <li v-for="task in tasks">{{ task }}</li>
  </ul>
  <button @click="toggle">Change</button>
</template>
<script setup>
import { ref } from "vue";

const name = ref("jobh");
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
</script>
