<template>
  <div class="min-h-screen flex flex-col items-center justify-center bg-gray-100 p-4">
    <h1 class="text-2xl font-bold mb-6">Flash Cards</h1>
    <ProgressBar :percent="progress" />
    <FlashCard
      :flashcard="flashcards[currentIndex]"
      :flipped="flipped"
      @flip="flipped = !flipped"
    />
    <div class="mt-6 flex justify-between w-full max-w-md">
      <button @click="prevCard" class="btn">‹ Previous</button>
      <span class="text-sm text-gray-600">{{ currentIndex + 1 }} of {{ flashcards.length }}</span>
      <button @click="nextCard" class="btn">Next ›</button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { flashcards } from './flashcards'
import FlashCard from './components/FlashCard.vue'
import ProgressBar from './components/ProgressBar.vue'


const currentIndex = ref(0)
const flipped = ref(false)

const progress = computed(() => {
  return Math.round(((currentIndex.value + 1) / flashcards.length) * 100)
})

function nextCard() {
  if (currentIndex.value < flashcards.length - 1) {
    currentIndex.value++
    flipped.value = false
  }
}

function prevCard() {
  if (currentIndex.value > 0) {
    currentIndex.value--
    flipped.value = false
  }
}
</script>

<style scoped>
.btn {
  @apply px-4 py-2 bg-white border rounded-lg text-sm shadow hover:bg-gray-50;
}
</style>
