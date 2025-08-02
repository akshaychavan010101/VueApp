<template>
  <h1>Hello {{ name }}</h1>
  <p v-if="status === 'deleted'">Yup the user is deleted</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else-if="status === 'active'">Yes active</p>
  <p v-else>user is inactive</p>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">
      {{ task }}
    </li>
  </ul>
  <a :href="link">Click to google</a>
  <br />
  <button @click="changeStatus">Change status</button>
</template>
<script>
export default {
  data() {
    return {
      name: "akshay",
      status: "pending",
      tasks: [1, 2, 3],
      link: "https://google.com",
    };
  },
  methods: {
    changeStatus() {
      if (this.status == "active") {
        this.status = "pending";
      } else if (this.status == "pending") {
        this.status = "inactive";
      } else {
        this.status = "active";
      }
    },
  },
};
</script>
<style scoped></style>
