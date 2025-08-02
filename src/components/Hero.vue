<template>
  <section class="bg-green-700 py-20 mb-4 mt-[1px]">
    <div class="text-center text-white">
      <h3 class="text-4xl font-bold">{{ title }}</h3>
      <p class="mt-2 font-bold">
        {{ subTitle }}
      </p>
    </div>
  </section>
</template>
<script setup>
const props = defineProps({
  title: {
    type: String,
    default: "Become a Vue Dev.",
  },
  subTitle: {
    type: String,
    default: "Find the Vue job that fits your skills and needs",
  },
});
</script>
