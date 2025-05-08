<template>
  <div class="max-w-xl mx-auto text-center mt-10 space-y-6">
    <!-- Barra de progreso -->
    <ProgressBar :current="currentIndex" :total="flashcards.length" />

    <!-- Transición con tarjeta -->
    <Transition name="fade" mode="out-in">
      <FlashCard
        :key="currentIndex"
        :question="currentCard.question"
        :answer="currentCard.answer"
        :flipped="flipped"
        @flip="toggleFlip"
      />
    </Transition>

    <!-- Navegación -->
    <div class="flex justify-between">
      <button
        @click="prevCard"
        :disabled="currentIndex === 0"
        class="px-4 py-2 bg-gray-300 text-gray-700 rounded disabled:opacity-50"
      >
        Anterior
      </button>
      <button
        @click="nextCard"
        :disabled="currentIndex === flashcards.length - 1"
        class="px-4 py-2 bg-blue-500 text-white rounded disabled:opacity-50"
      >
        Siguiente
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import FlashCard from './FlashCard.vue'
import ProgressBar from './ProgressBar.vue'
import { flashcards } from '../data/flashcards.js'

const currentIndex = ref(0)
const flipped = ref(false)

const currentCard = computed(() => flashcards[currentIndex.value])

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

function toggleFlip() {
  flipped.value = !flipped.value
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
