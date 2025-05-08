<template>
  <div
    class="relative w-full max-w-md p-6 bg-white border rounded-xl shadow-md transition-transform duration-700"
    :class="{ 'rotate-y-180': flipped }"
  >
    <div class="text-center">
      <p v-if="!flipped" class="font-semibold text-xl">{{ flashcard.question }}</p>
      <p v-else class="text-gray-700">{{ flashcard.answer }}</p>
    </div>
    <button class="mt-4 text-blue-500 underline" @click="$emit('flip')">
      {{ flipped ? 'Hide Answer' : 'Show Answer' }}
    </button>
  </div>
</template>

<script setup>
defineProps(['flashcard', 'flipped'])
defineEmits(['flip'])
</script>

<style scoped>
.rotate-y-180 {
  transform: rotateY(180deg);
}
</style>
