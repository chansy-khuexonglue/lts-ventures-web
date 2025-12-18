<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const words = ['Micro', 'Village', 'Diti']
const currentIndex = ref(0)
let intervalId: NodeJS.Timeout | null = null

onMounted(() => {
  // Change word every 3 seconds
  intervalId = setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % words.length
  }, 3000)
})

onUnmounted(() => {
  if (intervalId) {
    clearInterval(intervalId)
  }
})
</script>

<template>
  <div class="text-animation-wrapper">
    <div class="flex items-baseline gap-3">
      <!-- Animated rotating words -->
      <div class="word-slider">
        <div 
          class="word-track"
          :style="{ transform: `translateY(-${currentIndex * 100}%)` }"
        >
          <span 
            v-for="(word, index) in words" 
            :key="index"
            class="word-item text-4xl"
          >
            {{ word }}
          </span>
        </div>
      </div>
      
      <!-- Static word -->
      <span class="static-word">Banking</span>
    </div>
    
    <!-- Subtitle -->
    <div class="subtitle">
      Financing for Social Impact
    </div>
  </div>
</template>

<style scoped>
.text-animation-wrapper {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.word-slider {
  position: relative;
  height: 1em;
  overflow: hidden;
  display: inline-block;
  vertical-align: baseline;
}

.word-track {
  display: flex;
  flex-direction: column;
  transition: transform 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.word-item {
  display: block;
  line-height: 1;
  white-space: nowrap;
}

.static-word {
  display: inline-block;
  white-space: nowrap;
}

.subtitle {
  font-size: 0.875rem;
  opacity: 0.7;
  margin-top: 0.25rem;
}

/* Optional: Add color variation for each word */
.word-track .word-item:nth-child(1) {
  color: #3b82f6; /* blue */
}

.word-track .word-item:nth-child(2) {
  color: #8b5cf6; /* purple */
}

.word-track .word-item:nth-child(3) {
  color: #06b6d4; /* cyan */
}
</style>