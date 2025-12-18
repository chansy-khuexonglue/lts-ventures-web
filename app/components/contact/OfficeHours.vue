<script setup lang="ts">
type OfficeHour = {
  day: string;
  hours: string;
  isClosed?: boolean;
};

type Props = {
  schedule?: OfficeHour[];
};

const props = withDefaults(defineProps<Props>(), {
  schedule: () => [
    { day: "Monday - Friday", hours: "8:00 AM - 5:00 PM" },
    { day: "Saturday", hours: "8:00 AM - 12:00 PM" },
    { day: "Sunday", hours: "Closed", isClosed: true },
  ],
});
</script>

<template>
  <div class="bg-white dark:bg-gray-900 rounded-2xl p-8 shadow-lg">
    <h3
      class="text-xl font-bold text-gray-900 dark:text-white mb-6 flex items-center gap-2"
    >
      <UIcon name="i-lucide-calendar-clock" class="w-5 h-5" />
      Office Hours
    </h3>
    <div class="space-y-4">
      <div
        v-for="(item, index) in schedule"
        :key="index"
        class="flex justify-between items-center py-3"
        :class="{
          'border-b border-gray-200 dark:border-gray-800':
            index < schedule.length - 1,
        }"
      >
        <span class="text-gray-600 dark:text-gray-400">{{ item.day }}</span>
        <span
          class="font-semibold"
          :class="
            item.isClosed
              ? 'text-red-600 dark:text-red-400'
              : 'text-gray-900 dark:text-white'
          "
        >
          {{ item.hours }}
        </span>
      </div>
    </div>
  </div>
</template>
