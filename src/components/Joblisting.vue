<template>
  <div class="bg-white rounded-xl shadow-md relative">
    <div class="px-4 py-2">
      <div>
        <span class="text-gray-600 py-1 px-2 bg-gray-200">
          {{ job.type }}
        </span>
        <h3 class="text-xl font-bold my-2">{{ job.title }}</h3>
      </div>
      <div class="mb-5">
        <div>
          {{ truncatedDesc }}
        </div>
        <button
          @click="toggleDesc"
          class="text-green-500 text-sm hover:text-green-600"
        >
          {{ showFullDesc ? "Less" : "More" }}
        </button>
      </div>
      <h3 class="text-green-600 font-bold">{{ job.salary }}</h3>
      <hr class="text-gray-200 my-2 font-bold" />
      <div class="flex justify-between items-center">
        <p class="text-red-700 font-bold">
          <i class="pi pi-map-marker text-orange-700"></i>
          {{ job.location || "" }}
        </p>
        <RouterLink
          :to="'/jobs/' + job.id"
          class="rounded-xl bg-green-600 py-2 px-4 inline-block text-center text-white hover:bg-green-700"
        >
          Read More
        </RouterLink>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, computed } from "vue";
import { RouterLink } from "vue-router";
const showFullDesc = ref(false);
const truncatedDesc = computed(() => {
  let desc = props.job.description;
  if (!showFullDesc.value) {
    desc = desc.substring(0, 90) + "...";
  }
  return desc;
});
const toggleDesc = () => {
  showFullDesc.value = !showFullDesc.value;
};
const props = defineProps({
  job: {
    type: Object,
    default: {
      title: "Senior Vue Dev",
      type: "Full-Time",
      location: "Boston, MA",
      description:
        "We are seeking a talented Front-End Developer to join our team in Boston, MA. The ideal candidate will have strong skills in HTML, CSS, and JavaScript, with experience working with modern JavaScript frameworks such as Vue or Angular.",
      salary: "$90K - $100K / Year",
      company: {
        name: "NewTek Solutions",
        description:
          "NewTek Solutions is a leading technology company specializing in web development and digital solutions. We pride ourselves on delivering high-quality products and services to our clients while fostering a collaborative and innovative work environment.",
        contactEmail: "contact@teksolutions.com",
        contactPhone: "555-555-5555",
      },
      id: "1",
    },
  },
});
</script>
