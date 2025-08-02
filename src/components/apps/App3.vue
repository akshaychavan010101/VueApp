<template>
  <h1>{{ name }}</h1>
  <p v-if="status == 'active'">active</p>
  <p v-else-if="status == 'pending'">not</p>
  <p v-else-if="status == 'inactive'">yup</p>
  <p v-else>no</p>
  <button @click="toggle">Change</button>
</template>
<script>
import { ref } from "vue";

export default {
  setup() {
    const name = ref("akshay");
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

    return {
      name,
      status,
      tasks,
      toggle,
    };
  },
};
</script>
