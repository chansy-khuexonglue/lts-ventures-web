<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits<{
  submit: [
    data: {
      name: string;
      email: string;
      phone: string;
      subject: string;
      message: string;
    }
  ];
}>();

const form = ref({
  name: "",
  email: "",
  phone: "",
  subject: "",
  message: "",
});

const isSubmitting = ref(false);
const submitSuccess = ref(false);

async function handleSubmit() {
  isSubmitting.value = true;

  // Simulate API call
  await new Promise((resolve) => setTimeout(resolve, 2000));

  // Emit the form data
  emit("submit", { ...form.value });

  // Reset form
  form.value = {
    name: "",
    email: "",
    phone: "",
    subject: "",
    message: "",
  };

  submitSuccess.value = true;
  isSubmitting.value = false;

  // Hide success message after 5 seconds
  setTimeout(() => {
    submitSuccess.value = false;
  }, 5000);
}
</script>

<template>
  <div
    class="bg-white dark:bg-gray-900 rounded-2xl p-6 md:p-8 border border-gray-100 dark:border-gray-800"
  >
    <!-- Header -->
    <div class="mb-8">
      <div class="flex items-center gap-3 mb-3">
        <div
          class="w-12 h-12 rounded-xl bg-gradient-to-br from-blue-500 to-purple-600 flex items-center justify-center"
        >
          <UIcon name="i-lucide-mail" class="w-6 h-6 text-white" />
        </div>
        <h2
          class="text-2xl md:text-3xl font-bold text-gray-900 dark:text-white"
        >
          Send us a Message
        </h2>
      </div>
      <p class="text-gray-600 dark:text-gray-400 text-sm md:text-base">
        Fill out the form below and we'll get back to you as soon as possible.
      </p>
    </div>

    <!-- Success Message -->
    <div
      v-if="submitSuccess"
      class="mb-6 p-4 bg-green-50 dark:bg-green-900/20 border border-green-200 dark:border-green-800 rounded-xl animate-fade-in"
    >
      <div class="flex items-center gap-3">
        <UIcon
          name="i-lucide-check-circle"
          class="w-5 h-5 text-green-600 dark:text-green-400 flex-shrink-0"
        />
        <p class="text-green-800 dark:text-green-200 font-medium text-sm">
          Thank you! Your message has been sent successfully.
        </p>
      </div>
    </div>

    <!-- Form -->
    <form @submit.prevent="handleSubmit" class="space-y-5">
      <!-- Name & Email Row -->
      <div class="grid md:grid-cols-2 gap-5">
        <!-- Name -->
        <div class="w-full">
          <label
            class="block text-sm font-semibold text-gray-700 dark:text-gray-300 mb-2"
          >
            Full Name <span class="text-red-500">*</span>
          </label>
          <UInput
            v-model="form.name"
            placeholder="John Doe"
            size="xl"
            required
            icon="i-lucide-user"
            class="w-full"
          />
        </div>

        <!-- Email -->
        <div class="w-full">
          <label
            class="block text-sm font-semibold text-gray-700 dark:text-gray-300 mb-2"
          >
            Email Address <span class="text-red-500">*</span>
          </label>
          <UInput
            v-model="form.email"
            type="email"
            placeholder="john@example.com"
            size="xl"
            required
            icon="i-lucide-mail"
            class="w-full"
          />
        </div>
      </div>

      <!-- Phone & Subject Row -->
      <div class="grid md:grid-cols-2 gap-5">
        <!-- Phone -->
        <div class="w-full">
          <label
            class="block text-sm font-semibold text-gray-700 dark:text-gray-300 mb-2"
          >
            Phone Number
          </label>
          <UInput
            v-model="form.phone"
            type="tel"
            placeholder="+856 20 xxx xxx xx"
            size="xl"
            icon="i-lucide-phone"
            class="w-full"
          />
        </div>

        <!-- Subject -->
        <div class="w-full">
          <label
            class="block text-sm font-semibold text-gray-700 dark:text-gray-300 mb-2"
          >
            Subject <span class="text-red-500">*</span>
          </label>
          <UInput
            v-model="form.subject"
            placeholder="How can we help you?"
            size="xl"
            required
            icon="i-lucide-message-square"
            class="w-full"
          />
        </div>
      </div>

      <!-- Message -->
      <div class="w-full">
        <label
          class="block text-sm font-semibold text-gray-700 dark:text-gray-300 mb-2"
        >
          Message <span class="text-red-500">*</span>
        </label>
        <UTextarea
          v-model="form.message"
          placeholder="Tell us more about your inquiry..."
          :rows="6"
          required
          class="w-full"
          size="xl"
        />
      </div>

      <!-- Submit Button -->
      <div class="pt-2">
        <UButton
          type="submit"
          size="xl"
          color="primary"
          block
          :loading="isSubmitting"
          :disabled="isSubmitting"
          class="w-full transition-all hover:scale-[1.02]"
        >
          <template #leading>
            <UIcon name="i-lucide-send" class="w-5 h-5" />
          </template>
          {{ isSubmitting ? "Sending..." : "Send Message" }}
        </UButton>
      </div>

      <!-- Helper Text -->
      <p class="text-xs text-gray-500 dark:text-gray-400 text-center pt-2">
        We typically respond within 2 business hours during office hours.
      </p>
    </form>
  </div>
</template>

<style scoped>
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fade-in {
  animation: fadeIn 0.3s ease-out;
}

/* Ensure all inputs are full width */
:deep(.UInput),
:deep(.UTextarea) {
  width: 100%;
}
</style>
