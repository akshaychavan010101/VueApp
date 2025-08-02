<template>
  <nav class="bg-green-700">
    <div class="flex h-20 items-center justify-between">
      <div
        class="flex flex-1 items-center justify-center md:items-stretch md:justify-start"
      >
        <RouterLink to="/" class="flex flex-shrink-0 items-center mx-4 gap-2">
          <img :src="logo" class="h-10 w-10 rounded-[100%]" alt="Vie Jobs" />
          <span class="text-white text-2xl font-extrabold">Vue Jobs</span>
        </RouterLink>
        <div class="md:ml-auto">
          <div class="flex space-x-2 mr-4">
            <RouterLink
              to="/"
              :class="[
                isActiveLink('/')
                  ? 'bg-green-900'
                  : 'hover:bg-gray-900 hover:text-white',
                'text-white   rounded-md px-3 py-2',
              ]"
              >Home</RouterLink
            >
            <RouterLink
              to="/jobs"
              :class="[
                isActiveLink('/jobs')
                  ? 'bg-green-900'
                  : 'hover:bg-gray-900 hover:text-white',
                'text-white   rounded-md px-3 py-2',
              ]"
            >
              Jobs
            </RouterLink>
            <RouterLink
              to="/jobs/add"
              :class="[
                isActiveLink('/jobs/add')
                  ? 'bg-green-900'
                  : 'hover:bg-gray-900 hover:text-white',
                'text-white   rounded-md px-3 py-2',
              ]"
            >
              Add Job
            </RouterLink>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>
<script setup>
import logo from "@/assets/img/logo.png";
import { RouterLink, useRoute } from "vue-router";
const isActiveLink = (routePath) => {
  const route = useRoute();
  return route.path === routePath;
};
</script>
