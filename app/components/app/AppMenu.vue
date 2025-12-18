<script setup lang="ts">
type Props = {
  isMobile: boolean;
};

const props = defineProps<Props>();
const items = ref([
  {
    label: "Who We Are",
    icon: "i-lucide-book-open",
    children: [
      {
        label: "About Us",
        description: "Fully styled and customizable components for Nuxt.",
        icon: "i-lucide-house",
        to: "/docs/composables/define-shortcuts",
      },
      {
        label: "Management Team",
        description:
          "Learn how to install and configure Nuxt UI in your application.",
        icon: "i-lucide-cloud-download",
      },
      {
        label: "Awards",
        icon: "i-lucide-smile",
        description:
          "You have nothing to do, @nuxt/icon will handle it automatically.",
      },
      {
        label: "Publications",
        icon: "i-lucide-swatch-book",
        description:
          "Choose a primary and a neutral color from your Tailwind CSS theme.",
      },
    ],
  },
  {
    label: "What We Do",
    icon: "i-lucide-database",
    to: "/docs/composables",
    children: [
      {
        label: "Village Banking",
        icon: "i-lucide-file-text",
        description: "Define shortcuts for your application.",
        to: "/docs/composables/define-shortcuts",
      },
      {
        label: "Village's Feedback",
        icon: "i-lucide-file-text",
        description: "Display a modal/slideover within your application.",
        to: "/docs/composables/use-overlay",
      },
      {
        label: "LTS Growth",
        icon: "i-lucide-file-text",
        description: "Display a toast within your application.",
        to: "/docs/composables/use-toast",
      },
      {
        label: "Projects",
        icon: "i-lucide-file-text",
        description: "Display a toast within your application.",
        to: "/docs/composables/use-toast",
      },
      {
        label: "Trainings",
        icon: "i-lucide-file-text",
        description: "Display a toast within your application.",
        to: "/docs/composables/use-toast",
      },
    ],
  },
  {
    label: "Lan Xang Banker",
    icon: "i-lucide-box",
    to: "/docs/components",
    children: [
      {
        label: "Lan Xang Banker Platform",
        icon: "i-lucide-file-text",
        description: "Use NuxtLink with superpowers.",
        to: "/docs/components/link",
      },
      {
        label: "Credit Scoring",
        icon: "i-lucide-file-text",
        description: "Display a modal within your application.",
        to: "/docs/components/modal",
      },
      {
        label: "AI Loan Decisioning & Automation",
        icon: "i-lucide-file-text",
        description: "Display a list of links.",
        to: "/docs/components/navigation-menu",
      },
      {
        label: "Pagination",
        icon: "i-lucide-file-text",
        description: "Display a list of pages.",
        to: "/docs/components/pagination",
      },
      {
        label: "Popover",
        icon: "i-lucide-file-text",
        description:
          "Display a non-modal dialog that floats around a trigger element.",
        to: "/docs/components/popover",
      },
      {
        label: "Progress",
        icon: "i-lucide-file-text",
        description: "Show a horizontal bar to indicate task progression.",
        to: "/docs/components/progress",
      },
    ],
  },
  {
    label: "Career",
    icon: "material-symbols:work-outline",
    to: "/careers",
  },
]);
</script>

<template>
  <UNavigationMenu
    :items="items"
    arrow
    :orientation="props.isMobile ? 'vertical' : 'horizontal'"
  />
</template>
