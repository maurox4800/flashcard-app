<template>
  <div class="w-full bg-gray-200 rounded-full h-3 mb-4">
    <div
      class="bg-blue-500 h-3 rounded-full transition-all duration-300"
      :style="{ width: percent + '%' }"
    ></div>
  </div>
</template>

<script setup>
defineProps(['percent'])
</script>
