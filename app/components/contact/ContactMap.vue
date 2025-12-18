<script setup lang="ts">
type Props = {
  mapUrl?: string;
  address?: string;
  locationName?: string;
};

const props = withDefaults(defineProps<Props>(), {
  mapUrl:
    "https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3781.7429469524845!2d102.60999831490034!3d17.975706887789!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x31245d2f1e1e1e1f%3A0x1e1e1e1e1e1e1e1e!2sVientiane%2C%20Laos!5e0!3m2!1sen!2s!4v1234567890123!5m2!1sen!2s",
  address: "Chanthabouly District, Vientiane Capital, Lao PDR",
  locationName: "LTS Venture Head Office",
});
</script>

<template>
  <div
    class="bg-white dark:bg-gray-900 rounded-2xl overflow-hidden border border-gray-100 dark:border-gray-800"
  >
    <div class="p-6 border-b border-gray-200 dark:border-gray-800">
      <h3
        class="text-xl font-bold text-gray-900 dark:text-white flex items-center gap-2"
      >
        <UIcon name="i-lucide-map" class="w-5 h-5" />
        Our Location
      </h3>
    </div>
    <div class="relative h-96">
      <!-- Google Maps Embed -->
      <iframe
        :src="mapUrl"
        width="100%"
        height="100%"
        style="border: 0"
        loading="lazy"
        referrerpolicy="no-referrer-when-downgrade"
        class="w-full h-full"
      />
    </div>
    <div class="p-6">
      <div class="flex items-start gap-3">
        <UIcon
          name="i-lucide-navigation"
          class="w-5 h-5 text-blue-600 dark:text-blue-400 mt-1"
        />
        <div>
          <p class="font-medium text-gray-900 dark:text-white mb-1">
            {{ locationName }}
          </p>
          <p class="text-gray-600 dark:text-gray-400 text-sm">
            {{ address }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
