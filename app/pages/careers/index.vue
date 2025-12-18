<script setup lang="ts">
import { ref, onMounted } from "vue";

// SEO
const title = "Careers - Join Our Team | LTS Venture";
const description =
  "Join LTS Venture and make a difference in communities across Laos. Explore career opportunities in microfinance, technology, and community development.";

useSeoMeta({
  title,
  description,
  ogTitle: title,
  ogDescription: description,
  ogImage: "/og-image.png",
  twitterCard: "summary_large_image",
});

// Job openings
const jobOpenings = [
  {
    id: 1,
    title: "Senior Loan Officer",
    department: "Microfinance",
    location: "Vientiane",
    type: "Full-time",
    experience: "3-5 years",
    description:
      "Lead our microfinance operations and help empower rural communities through sustainable lending practices.",
    requirements: [
      "Bachelor's degree in Finance, Economics, or related field",
      "3+ years of experience in microfinance or banking",
      "Strong understanding of loan assessment and risk management",
      "Excellent communication skills in Lao and English",
    ],
  },
  {
    id: 2,
    title: "Mobile App Developer",
    department: "Technology",
    location: "Vientiane",
    type: "Full-time",
    experience: "2-4 years",
    description:
      "Build and maintain our Lan Xang Banker mobile application to bring digital banking to rural communities.",
    requirements: [
      "Experience with React Native or Flutter",
      "Strong knowledge of mobile app development best practices",
      "Understanding of financial technology and security",
      "Portfolio of published mobile applications",
    ],
  },
  {
    id: 3,
    title: "Community Development Specialist",
    department: "Operations",
    location: "Multiple Locations",
    type: "Full-time",
    experience: "2-3 years",
    description:
      "Work directly with village communities to implement training programs and development initiatives.",
    requirements: [
      "Degree in Social Work, Development Studies, or related field",
      "Experience working with rural communities",
      "Strong interpersonal and training skills",
      "Willingness to travel to remote areas",
    ],
  },
  {
    id: 4,
    title: "Financial Analyst",
    department: "Finance",
    location: "Vientiane",
    type: "Full-time",
    experience: "1-3 years",
    description:
      "Analyze financial data and provide insights to support strategic decision-making.",
    requirements: [
      "Bachelor's degree in Finance, Accounting, or Economics",
      "Proficiency in Excel and financial modeling",
      "Strong analytical and problem-solving skills",
      "Attention to detail and accuracy",
    ],
  },
  {
    id: 5,
    title: "Marketing Coordinator",
    department: "Marketing",
    location: "Vientiane",
    type: "Full-time",
    experience: "1-2 years",
    description:
      "Develop and execute marketing campaigns to promote our services and increase community awareness.",
    requirements: [
      "Degree in Marketing, Communications, or related field",
      "Experience with digital marketing and social media",
      "Creative thinking and content creation skills",
      "Fluency in Lao and English",
    ],
  },
  {
    id: 6,
    title: "IT Support Specialist",
    department: "Technology",
    location: "Vientiane",
    type: "Full-time",
    experience: "1-2 years",
    description:
      "Provide technical support and maintain IT infrastructure across our offices.",
    requirements: [
      "Knowledge of computer hardware and software troubleshooting",
      "Experience with network administration",
      "Customer service orientation",
      "Ability to work independently and as part of a team",
    ],
  },
];

// Benefits
const benefits = [
  {
    icon: "i-lucide-heart",
    title: "Health Insurance",
    description: "Comprehensive health coverage for you and your family",
  },
  {
    icon: "i-lucide-graduation-cap",
    title: "Learning & Development",
    description:
      "Continuous training and professional development opportunities",
  },
  {
    icon: "i-lucide-calendar",
    title: "Flexible Schedule",
    description: "Work-life balance with flexible working arrangements",
  },
  {
    icon: "i-lucide-trending-up",
    title: "Career Growth",
    description: "Clear career progression paths and promotion opportunities",
  },
  {
    icon: "i-lucide-users",
    title: "Team Culture",
    description: "Collaborative and inclusive work environment",
  },
  {
    icon: "i-lucide-gift",
    title: "Competitive Salary",
    description: "Market-competitive compensation and performance bonuses",
  },
];

// Selected job for modal
const selectedJob = ref<(typeof jobOpenings)[0] | null>(null);
const isModalOpen = ref(false);

function openJobModal(job: (typeof jobOpenings)[0]) {
  selectedJob.value = job;
  isModalOpen.value = true;
}

function closeJobModal() {
  isModalOpen.value = false;
  selectedJob.value = null;
}

// Animation state
const isVisible = ref({
  benefits: false,
  jobs: false,
  cta: false,
});

// Intersection Observer for scroll animations
onMounted(() => {
  const observerOptions = {
    threshold: 0.1,
    rootMargin: "0px 0px -100px 0px",
  };

  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        const target = entry.target.getAttribute("data-section");
        if (target) {
          isVisible.value[target as keyof typeof isVisible.value] = true;
        }
      }
    });
  }, observerOptions);

  // Observe all sections
  document.querySelectorAll("[data-section]").forEach((section) => {
    observer.observe(section);
  });
});
</script>

<template>
  <div class="min-h-screen bg-gray-50 dark:bg-gray-950">
    <!-- Hero Section -->
    <section
      class="relative py-24 md:py-32 bg-gradient-to-br from-blue-600 via-purple-600 to-pink-600 overflow-hidden"
    >
      <!-- Background Pattern -->
      <div class="absolute inset-0 opacity-10">
        <div
          class="absolute inset-0"
          style="
            background-image: radial-gradient(
              circle at 2px 2px,
              rgba(255, 255, 255, 0.15) 1px,
              transparent 0
            );
            background-size: 50px 50px;
          "
        />
      </div>

      <div class="container mx-auto px-4 relative z-10">
        <div class="text-center max-w-4xl mx-auto">
          <div
            class="inline-flex items-center justify-center w-20 h-20 rounded-full bg-white/10 backdrop-blur-sm mb-6"
          >
            <UIcon name="i-lucide-briefcase" class="w-10 h-10 text-white" />
          </div>
          <h1
            class="text-5xl md:text-7xl font-bold text-white mb-6 leading-tight"
          >
            Join Our Mission
          </h1>
          <p class="text-xl md:text-2xl text-white/90 mb-8">
            Build your career while making a real difference in communities
            across Laos. We're looking for passionate individuals to join our
            team.
          </p>
          <div class="flex flex-wrap justify-center gap-4">
            <UButton
              size="xl"
              color="neutral"
              variant="solid"
              to="#openings"
              icon="i-lucide-search"
            >
              View Open Positions
            </UButton>
            <UButton
              size="xl"
              color="neutral"
              variant="outline"
              to="#culture"
              icon="i-lucide-heart"
            >
              Our Culture
            </UButton>
          </div>
        </div>
      </div>
    </section>

    <!-- Stats Section -->
    <section class="py-16 -mt-36 relative z-20">
      <div class="container mx-auto px-4">
        <div
          class="bg-white dark:bg-gray-900 shadow-lg rounded-2xl p-8 md:p-12 border border-gray-100 dark:border-gray-800"
        >
          <div class="grid md:grid-cols-4 gap-8">
            <div class="text-center">
              <div class="text-4xl font-bold text-blue-600 mb-2">200+</div>
              <div class="text-gray-600 dark:text-gray-400">Team Members</div>
            </div>
            <div class="text-center">
              <div class="text-4xl font-bold text-purple-600 mb-2">15+</div>
              <div class="text-gray-600 dark:text-gray-400">Offices</div>
            </div>
            <div class="text-center">
              <div class="text-4xl font-bold text-pink-600 mb-2">50+</div>
              <div class="text-gray-600 dark:text-gray-400">Years Combined</div>
            </div>
            <div class="text-center">
              <div class="text-4xl font-bold text-orange-600 mb-2">95%</div>
              <div class="text-gray-600 dark:text-gray-400">
                Satisfaction Rate
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Benefits Section -->
    <section
      id="culture"
      class="py-20 bg-white dark:bg-gray-900"
      data-section="benefits"
    >
      <div class="container mx-auto px-4">
        <div class="text-center mb-12">
          <h2
            class="text-3xl md:text-5xl font-bold text-gray-900 dark:text-white mb-4"
          >
            Why Work With Us
          </h2>
          <p class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">
            We invest in our people and create an environment where you can
            thrive
          </p>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div
            v-for="(benefit, index) in benefits"
            :key="index"
            class="bg-gray-50 dark:bg-gray-800 rounded-2xl p-6 border border-gray-100 dark:border-gray-700 hover:-translate-y-2 transition-all duration-300"
            :class="isVisible.benefits ? 'animate-fade-in-up' : 'opacity-0'"
            :style="{ animationDelay: `${index * 100}ms` }"
          >
            <div
              class="w-12 h-12 rounded-xl bg-gradient-to-br from-blue-500 to-purple-600 flex items-center justify-center mb-4"
            >
              <UIcon :name="benefit.icon" class="w-6 h-6 text-white" />
            </div>
            <h3 class="text-xl font-bold text-gray-900 dark:text-white mb-2">
              {{ benefit.title }}
            </h3>
            <p class="text-gray-600 dark:text-gray-400">
              {{ benefit.description }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Job Openings Section -->
    <section id="openings" class="py-20" data-section="jobs">
      <div class="container mx-auto px-4">
        <div class="text-center mb-12">
          <h2
            class="text-3xl md:text-5xl font-bold text-gray-900 dark:text-white mb-4"
          >
            Open Positions
          </h2>
          <p class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">
            Find your next opportunity and join our growing team
          </p>
        </div>

        <div
          class="max-w-4xl mx-auto space-y-4"
          :class="isVisible.jobs ? 'animate-fade-in-up' : 'opacity-0'"
        >
          <div
            v-for="job in jobOpenings"
            :key="job.id"
            class="bg-white dark:bg-gray-900 rounded-2xl p-6 border border-gray-100 dark:border-gray-800 hover:border-blue-500 dark:hover:border-blue-500 transition-all cursor-pointer group"
            @click="openJobModal(job)"
          >
            <div
              class="flex flex-col md:flex-row md:items-center md:justify-between gap-4"
            >
              <div class="flex-1">
                <h3
                  class="text-xl font-bold text-gray-900 dark:text-white mb-2 group-hover:text-blue-600 dark:group-hover:text-blue-400 transition-colors"
                >
                  {{ job.title }}
                </h3>
                <p class="text-gray-600 dark:text-gray-400 mb-3">
                  {{ job.description }}
                </p>
                <div class="flex flex-wrap gap-2">
                  <span
                    class="inline-flex items-center gap-1 px-3 py-1 rounded-full bg-blue-50 dark:bg-blue-900/20 text-blue-600 dark:text-blue-400 text-sm"
                  >
                    <UIcon name="i-lucide-briefcase" class="w-4 h-4" />
                    {{ job.department }}
                  </span>
                  <span
                    class="inline-flex items-center gap-1 px-3 py-1 rounded-full bg-purple-50 dark:bg-purple-900/20 text-purple-600 dark:text-purple-400 text-sm"
                  >
                    <UIcon name="i-lucide-map-pin" class="w-4 h-4" />
                    {{ job.location }}
                  </span>
                  <span
                    class="inline-flex items-center gap-1 px-3 py-1 rounded-full bg-green-50 dark:bg-green-900/20 text-green-600 dark:text-green-400 text-sm"
                  >
                    <UIcon name="i-lucide-clock" class="w-4 h-4" />
                    {{ job.type }}
                  </span>
                  <span
                    class="inline-flex items-center gap-1 px-3 py-1 rounded-full bg-orange-50 dark:bg-orange-900/20 text-orange-600 dark:text-orange-400 text-sm"
                  >
                    <UIcon name="i-lucide-award" class="w-4 h-4" />
                    {{ job.experience }}
                  </span>
                </div>
              </div>
              <div>
                <UButton
                  color="primary"
                  variant="soft"
                  icon="i-lucide-arrow-right"
                  trailing
                >
                  View Details
                </UButton>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section
      class="py-20 bg-gradient-to-br from-blue-600 to-purple-600"
      data-section="cta"
    >
      <div
        class="container mx-auto px-4 text-center"
        :class="isVisible.cta ? 'animate-fade-in-up' : 'opacity-0'"
      >
        <h2 class="text-3xl md:text-5xl font-bold text-white mb-6">
          Don't See the Right Position?
        </h2>
        <p class="text-xl text-white/90 mb-8 max-w-2xl mx-auto">
          We're always looking for talented individuals. Send us your resume and
          we'll keep you in mind for future opportunities.
        </p>
        <UButton
          size="xl"
          color="neutral"
          variant="solid"
          to="/contact-us"
          icon="i-lucide-send"
        >
          Send Your Resume
        </UButton>
      </div>
    </section>

    <!-- Job Details Modal -->
    <UModal v-model="isModalOpen" :ui="{ wrapper: 'max-w-3xl' }">
      <div v-if="selectedJob" class="p-6">
        <div class="flex items-start justify-between mb-6">
          <div>
            <h2
              class="text-2xl md:text-3xl font-bold text-gray-900 dark:text-white mb-2"
            >
              {{ selectedJob.title }}
            </h2>
            <div class="flex flex-wrap gap-2">
              <span
                class="inline-flex items-center gap-1 px-3 py-1 rounded-full bg-blue-50 dark:bg-blue-900/20 text-blue-600 dark:text-blue-400 text-sm"
              >
                <UIcon name="i-lucide-briefcase" class="w-4 h-4" />
                {{ selectedJob.department }}
              </span>
              <span
                class="inline-flex items-center gap-1 px-3 py-1 rounded-full bg-purple-50 dark:bg-purple-900/20 text-purple-600 dark:text-purple-400 text-sm"
              >
                <UIcon name="i-lucide-map-pin" class="w-4 h-4" />
                {{ selectedJob.location }}
              </span>
            </div>
          </div>
          <UButton
            color="neutral"
            variant="ghost"
            icon="i-lucide-x"
            square
            @click="closeJobModal"
          />
        </div>

        <div class="space-y-6">
          <div>
            <h3 class="text-lg font-bold text-gray-900 dark:text-white mb-3">
              Job Description
            </h3>
            <p class="text-gray-600 dark:text-gray-400">
              {{ selectedJob.description }}
            </p>
          </div>

          <div>
            <h3 class="text-lg font-bold text-gray-900 dark:text-white mb-3">
              Requirements
            </h3>
            <ul class="space-y-2">
              <li
                v-for="(req, index) in selectedJob.requirements"
                :key="index"
                class="flex items-start gap-2 text-gray-600 dark:text-gray-400"
              >
                <UIcon
                  name="i-lucide-check-circle"
                  class="w-5 h-5 text-green-600 dark:text-green-400 flex-shrink-0 mt-0.5"
                />
                <span>{{ req }}</span>
              </li>
            </ul>
          </div>

          <div class="pt-4 border-t border-gray-200 dark:border-gray-800">
            <UButton
              size="xl"
              color="primary"
              block
              icon="i-lucide-send"
              to="/contact-us"
            >
              Apply for this Position
            </UButton>
          </div>
        </div>
      </div>
    </UModal>
  </div>
</template>

<style scoped>
/* Smooth scrolling */
html {
  scroll-behavior: smooth;
}

/* Fade in animations */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-fade-in-up {
  animation: fadeInUp 0.8s ease-out forwards;
}
</style>
