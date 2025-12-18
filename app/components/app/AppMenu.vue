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
        description:
          "Learn about our mission to empower communities through sustainable microfinance",
        icon: "i-lucide-house",
        to: "/about-us",
      },
      {
        label: "Management Team",
        description:
          "Meet the leaders driving innovation in rural financial services",
        icon: "i-lucide-users",
      },
      {
        label: "Awards",
        icon: "i-lucide-award",
        description:
          "Recognition for our impact in community development and microfinance",
      },
      {
        label: "Publications",
        icon: "i-lucide-book",
        description:
          "Research and insights on microfinance and rural development",
      },
    ],
  },
  {
    label: "What We Do",
    icon: "i-lucide-briefcase",
    to: "/what-we-do",
    children: [
      {
        label: "Village Banking",
        icon: "i-lucide-home",
        description:
          "Community-based financial services bringing banking to rural areas",
        to: "/what-we-do#village-banking",
      },
      {
        label: "Village's Feedback",
        icon: "i-lucide-message-square",
        description: "Real stories and testimonials from communities we serve",
        to: "/what-we-do#feedback",
      },
      {
        label: "LTS Growth",
        icon: "i-lucide-trending-up",
        description:
          "Sustainable growth programs for small businesses and entrepreneurs",
        to: "/what-we-do#growth",
      },
      {
        label: "Projects",
        icon: "i-lucide-folder",
        description:
          "Community development initiatives transforming rural Laos",
        to: "/what-we-do#projects",
      },
      {
        label: "Trainings",
        icon: "i-lucide-graduation-cap",
        description:
          "Financial literacy and entrepreneurship training programs",
        to: "/what-we-do#trainings",
      },
    ],
  },
  {
    label: "Lan Xang Banker",
    icon: "i-lucide-smartphone",
    to: "/lan-xang-banker",
    children: [
      {
        label: "Lan Xang Banker Platform",
        icon: "i-lucide-smartphone",
        description:
          "Digital banking platform bringing financial services to your mobile",
        to: "/lan-xang-banker",
      },
      {
        label: "Credit Scoring",
        icon: "i-lucide-chart-bar",
        description:
          "Advanced credit assessment for fair and transparent lending",
        to: "/lan-xang-banker#credit-scoring",
      },
      {
        label: "AI Loan Decisioning & Automation",
        icon: "i-lucide-brain",
        description:
          "Smart automation for faster, more accurate loan processing",
        to: "/lan-xang-banker#ai-decisioning",
      },
    ],
  },
  {
    label: "Career",
    icon: "i-lucide-briefcase",
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
