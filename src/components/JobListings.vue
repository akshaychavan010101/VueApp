<template>
  <section class="bg-blue-50">
    <div class="container-xxl lg:container m-auto p-4">
      <h2 class="text-3xl font-extrabold text-green-500 text-center mb-6">
        Browse Jobs
      </h2>

      <div v-if="isLoading" class="text-center text-gray-500 py-6">
        <PulseLoader />
      </div>
      <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <Joblisting
          v-for="job in jobs.slice(0, limit || jobs.length)"
          :key="job.id"
          :job="job"
        />
      </div>
    </div>
  </section>
  <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
    <RouterLink
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded hover"
    >
      View All Jobs
    </RouterLink>
  </section>
</template>
<script setup>
import axios from "axios";
import { onMounted, ref } from "vue";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import Joblisting from "@/components/Joblisting.vue";
import { RouterLink } from "vue-router";
const jobs = ref([]);
const isLoading = ref(true);

const props = defineProps({
  limit: {
    type: Number,
    default: 10,
  },
  showButton: {
    type: Boolean,
    default: false,
  },
});
const fetchList = async () => {
  try {
    const data = await axios.get("/api/jobs");
    jobs.value = data.data;
  } catch (error) {
    console.log("Error in fetching jobs", error);
  } finally {
    isLoading.value = false;
  }
};
onMounted(async () => {
  await fetchList();
});
</script>
