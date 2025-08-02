<template>
  <div :class="`${background} p-6 rounded-lg shadow-md mb-4`">
    <slot></slot>
  </div>
</template>
<script setup>
const props = defineProps({
  background: {
    type: String,
    default: "bg-gray-100",
  },
});
</script>
