<script setup lang="ts">
type Props = {
  icon: string;
  title: string;
  details: string[];
  color: string;
};

const props = defineProps<Props>();
</script>

<template>
  <div
    class="bg-white shadow-lg dark:bg-gray-900 rounded-2xl p-6 border border-gray-100 dark:border-gray-800 transition-all duration-300 hover:-translate-y-2"
  >
    <div
      class="inline-flex items-center justify-center w-14 h-14 rounded-xl mb-4 bg-gradient-to-br"
      :class="`from-${color}-400 to-${color}-600`"
    >
      <UIcon :name="icon" class="w-7 h-7 text-white" />
    </div>
    <h3 class="text-lg font-bold text-gray-900 dark:text-white mb-3">
      {{ title }}
    </h3>
    <div class="space-y-1">
      <p
        v-for="(detail, idx) in details"
        :key="idx"
        class="text-gray-600 dark:text-gray-400"
      >
        {{ detail }}
      </p>
    </div>
  </div>
</template>
