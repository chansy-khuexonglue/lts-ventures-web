<script setup lang="ts">
import { ref, onMounted } from "vue";

// SEO
const title = "Contact Us - LTS Venture";
const description =
  "Get in touch with LTS Venture. Visit our office, call us, or send us a message. We're here to help you with all your microfinance and community development needs.";

useSeoMeta({
  title,
  description,
  ogTitle: title,
  ogDescription: description,
  ogImage: "/og-image.png",
  twitterCard: "summary_large_image",
});

// Animation state
const isVisible = ref({
  cards: false,
  form: false,
  map: false,
  faq: false,
});

// Contact information
const contactInfo = [
  {
    icon: "i-lucide-map-pin",
    title: "Visit Us",
    details: ["Vientiane Capital, Laos", "Chanthabouly District"],
    color: "blue",
  },
  {
    icon: "i-lucide-phone",
    title: "Call Us",
    details: ["+856 21 123 456", "+856 20 987 654 32"],
    color: "green",
  },
  {
    icon: "i-lucide-mail",
    title: "Email Us",
    details: ["info@ltsventure.la", "support@ltsventure.la"],
    color: "purple",
  },
  {
    icon: "i-lucide-clock",
    title: "Working Hours",
    details: ["Mon - Fri: 8:00 AM - 5:00 PM", "Sat: 8:00 AM - 12:00 PM"],
    color: "orange",
  },
];

// Form submission handler
function handleFormSubmit(data: any) {
  console.log("Form submitted:", data);
  // Handle form submission (e.g., send to API)
}

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

  // Cards are visible immediately
  isVisible.value.cards = true;
});
</script>

<template>
  <div class="min-h-screen bg-gray-50 dark:bg-gray-950">
    <!-- Hero Section with Enhanced Design -->
    <section
      class="relative py-24 md:py-32 bg-gradient-to-br from-blue-600 via-purple-600 to-pink-600 overflow-hidden"
    >
      <!-- Animated Background -->
      <div class="absolute inset-0">
        <!-- Pattern Overlay -->
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

        <!-- Floating Shapes -->
        <div class="floating-shapes">
          <div class="shape shape-1" />
          <div class="shape shape-2" />
          <div class="shape shape-3" />
        </div>
      </div>

      <div class="container mx-auto px-4 relative z-10">
        <div class="text-center max-w-4xl mx-auto">
          <div
            class="inline-flex items-center justify-center w-20 h-20 rounded-full bg-white/10 backdrop-blur-sm mb-6 animate-bounce-slow"
          >
            <UIcon name="i-lucide-mail" class="w-10 h-10 text-white" />
          </div>
          <h1
            class="text-5xl md:text-7xl font-bold text-white mb-6 leading-tight animate-fade-in-up"
          >
            Let's Connect
          </h1>
          <p
            class="text-xl md:text-2xl text-white/90 mb-8 animate-fade-in-up"
            style="animation-delay: 0.1s"
          >
            We'd love to hear from you. Whether you have a question about our
            services, need assistance, or want to partner with us, our team is
            ready to help.
          </p>

          <!-- Quick Stats -->
          <div
            class="grid grid-cols-3 gap-4 md:gap-8 max-w-2xl mx-auto mt-12 animate-fade-in-up"
            style="animation-delay: 0.2s"
          >
            <div class="text-center">
              <div class="text-3xl md:text-4xl font-bold text-white mb-2">
                24/7
              </div>
              <div class="text-sm md:text-base text-white/80">Support</div>
            </div>
            <div class="text-center">
              <div class="text-3xl md:text-4xl font-bold text-white mb-2">
                &lt;2h
              </div>
              <div class="text-sm md:text-base text-white/80">
                Response Time
              </div>
            </div>
            <div class="text-center">
              <div class="text-3xl md:text-4xl font-bold text-white mb-2">
                100%
              </div>
              <div class="text-sm md:text-base text-white/80">Satisfaction</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Information Cards with Stagger Animation -->
    <section class="py-16 -mt-40 relative z-20" data-section="cards">
      <div class="container mx-auto px-4">
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
          <div
            v-for="(info, index) in contactInfo"
            :key="index"
            class="transform transition-all duration-500"
            :class="
              isVisible.cards
                ? 'translate-y-0 opacity-100'
                : 'translate-y-10 opacity-0'
            "
            :style="{ transitionDelay: `${index * 100}ms` }"
          >
            <ContactInfoCard
              :icon="info.icon"
              :title="info.title"
              :details="info.details"
              :color="info.color"
            />
          </div>
        </div>
      </div>
    </section>

    <!-- Main Content: Form + Map with Better Layout -->
    <section class="py-16" data-section="form">
      <div class="container mx-auto px-4">
        <div class="grid lg:grid-cols-5 gap-12">
          <!-- Contact Form - Takes 3 columns -->
          <div
            class="lg:col-span-3 space-y-8"
            :class="isVisible.form ? 'animate-fade-in-left' : 'opacity-0'"
          >
            <ContactForm @submit="handleFormSubmit" />

            <!-- Social Media -->
            <div
              class="bg-white dark:bg-gray-900 rounded-2xl p-8 border border-gray-100 dark:border-gray-800"
            >
              <h3
                class="text-xl font-bold text-gray-900 dark:text-white mb-4 flex items-center gap-2"
              >
                <UIcon name="i-lucide-share-2" class="w-5 h-5" />
                Connect With Us
              </h3>
              <p class="text-gray-600 dark:text-gray-400 mb-6">
                Follow us on social media for updates and news
              </p>
              <div class="flex flex-wrap gap-3">
                <UButton
                  icon="i-lucide-facebook"
                  size="lg"
                  color="neutral"
                  variant="soft"
                  square
                  class="hover:scale-110 transition-transform"
                />
                <UButton
                  icon="i-lucide-twitter"
                  size="lg"
                  color="neutral"
                  variant="soft"
                  square
                  class="hover:scale-110 transition-transform"
                />
                <UButton
                  icon="i-lucide-linkedin"
                  size="lg"
                  color="neutral"
                  variant="soft"
                  square
                  class="hover:scale-110 transition-transform"
                />
                <UButton
                  icon="i-lucide-instagram"
                  size="lg"
                  color="neutral"
                  variant="soft"
                  square
                  class="hover:scale-110 transition-transform"
                />
                <UButton
                  icon="i-lucide-youtube"
                  size="lg"
                  color="neutral"
                  variant="soft"
                  square
                  class="hover:scale-110 transition-transform"
                />
              </div>
            </div>
          </div>

          <!-- Map & Additional Info - Takes 2 columns -->
          <div
            class="lg:col-span-2 space-y-8"
            data-section="map"
            :class="isVisible.map ? 'animate-fade-in-right' : 'opacity-0'"
          >
            <!-- Map -->
            <ContactMap />

            <!-- Office Hours -->
            <OfficeHours />

            <!-- Quick Contact with Enhanced Design -->
            <div
              class="bg-gradient-to-br from-blue-600 to-purple-600 rounded-2xl p-8 text-white relative overflow-hidden"
            >
              <!-- Background Pattern -->
              <div class="absolute inset-0 opacity-10">
                <div
                  class="absolute inset-0"
                  style="
                    background-image: radial-gradient(
                      circle at 2px 2px,
                      rgba(255, 255, 255, 0.3) 1px,
                      transparent 0
                    );
                    background-size: 20px 20px;
                  "
                />
              </div>

              <div class="relative z-10">
                <div class="flex items-center gap-3 mb-4">
                  <div
                    class="w-12 h-12 rounded-full bg-white/20 backdrop-blur-sm flex items-center justify-center"
                  >
                    <UIcon name="i-lucide-headphones" class="w-6 h-6" />
                  </div>
                  <h3 class="text-2xl font-bold">Need Immediate Assistance?</h3>
                </div>
                <p class="text-white/90 mb-6">
                  Our customer support team is available during business hours
                  to help you with any urgent matters.
                </p>
                <div class="space-y-3">
                  <a
                    href="tel:+85621123456"
                    class="flex items-center gap-3 p-4 bg-white/10 backdrop-blur-sm rounded-lg hover:bg-white/20 transition-all hover:scale-105"
                  >
                    <div
                      class="w-10 h-10 rounded-full bg-white/20 flex items-center justify-center flex-shrink-0"
                    >
                      <UIcon name="i-lucide-phone-call" class="w-5 h-5" />
                    </div>
                    <div>
                      <div class="text-sm text-white/80">Call us now</div>
                      <div class="font-semibold">+856 21 123 456</div>
                    </div>
                  </a>
                  <a
                    href="mailto:info@ltsventure.la"
                    class="flex items-center gap-3 p-4 bg-white/10 backdrop-blur-sm rounded-lg hover:bg-white/20 transition-all hover:scale-105"
                  >
                    <div
                      class="w-10 h-10 rounded-full bg-white/20 flex items-center justify-center flex-shrink-0"
                    >
                      <UIcon name="i-lucide-mail" class="w-5 h-5" />
                    </div>
                    <div>
                      <div class="text-sm text-white/80">Email us</div>
                      <div class="font-semibold">info@ltsventure.la</div>
                    </div>
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- FAQ Section with Enhanced Design -->
    <section class="py-20 bg-white dark:bg-gray-900" data-section="faq">
      <div class="container mx-auto px-4">
        <div
          class="text-center mb-12"
          :class="isVisible.faq ? 'animate-fade-in-up' : 'opacity-0'"
        >
          <div
            class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-gradient-to-br from-blue-500 to-purple-600 mb-6"
          >
            <UIcon name="i-lucide-help-circle" class="w-8 h-8 text-white" />
          </div>
          <h2
            class="text-3xl md:text-5xl font-bold text-gray-900 dark:text-white mb-4"
          >
            Frequently Asked Questions
          </h2>
          <p class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">
            Find quick answers to common questions about our services
          </p>
        </div>

        <div
          class="max-w-3xl mx-auto space-y-4"
          :class="isVisible.faq ? 'animate-fade-in-up' : 'opacity-0'"
          style="animation-delay: 0.2s"
        >
          <details
            class="group bg-gray-50 dark:bg-gray-800 rounded-xl p-6 cursor-pointer hover:shadow-lg transition-all"
          >
            <summary
              class="flex justify-between items-center font-semibold text-gray-900 dark:text-white"
            >
              <span class="flex items-center gap-3">
                <UIcon
                  name="i-lucide-briefcase"
                  class="w-5 h-5 text-blue-600"
                />
                What services does LTS Venture offer?
              </span>
              <UIcon
                name="i-lucide-chevron-down"
                class="w-5 h-5 group-open:rotate-180 transition-transform text-blue-600"
              />
            </summary>
            <p class="mt-4 text-gray-600 dark:text-gray-400 pl-8">
              We offer village banking, microfinance solutions, digital banking
              through Lan Xang Banker, training programs, and community
              development projects.
            </p>
          </details>

          <details
            class="group bg-gray-50 dark:bg-gray-800 rounded-xl p-6 cursor-pointer hover:shadow-lg transition-all"
          >
            <summary
              class="flex justify-between items-center font-semibold text-gray-900 dark:text-white"
            >
              <span class="flex items-center gap-3">
                <UIcon name="i-lucide-coins" class="w-5 h-5 text-green-600" />
                How can I apply for a microloan?
              </span>
              <UIcon
                name="i-lucide-chevron-down"
                class="w-5 h-5 group-open:rotate-180 transition-transform text-green-600"
              />
            </summary>
            <p class="mt-4 text-gray-600 dark:text-gray-400 pl-8">
              You can visit our office during business hours or contact us
              through this form. Our team will guide you through the application
              process.
            </p>
          </details>

          <details
            class="group bg-gray-50 dark:bg-gray-800 rounded-xl p-6 cursor-pointer hover:shadow-lg transition-all"
          >
            <summary
              class="flex justify-between items-center font-semibold text-gray-900 dark:text-white"
            >
              <span class="flex items-center gap-3">
                <UIcon
                  name="i-lucide-graduation-cap"
                  class="w-5 h-5 text-purple-600"
                />
                Do you provide training programs?
              </span>
              <UIcon
                name="i-lucide-chevron-down"
                class="w-5 h-5 group-open:rotate-180 transition-transform text-purple-600"
              />
            </summary>
            <p class="mt-4 text-gray-600 dark:text-gray-400 pl-8">
              Yes! We offer comprehensive financial education and
              entrepreneurship training programs for community members. Contact
              us to learn more about upcoming sessions.
            </p>
          </details>

          <details
            class="group bg-gray-50 dark:bg-gray-800 rounded-xl p-6 cursor-pointer hover:shadow-lg transition-all"
          >
            <summary
              class="flex justify-between items-center font-semibold text-gray-900 dark:text-white"
            >
              <span class="flex items-center gap-3">
                <UIcon name="i-lucide-clock" class="w-5 h-5 text-orange-600" />
                What are your response times?
              </span>
              <UIcon
                name="i-lucide-chevron-down"
                class="w-5 h-5 group-open:rotate-180 transition-transform text-orange-600"
              />
            </summary>
            <p class="mt-4 text-gray-600 dark:text-gray-400 pl-8">
              We typically respond to all inquiries within 2 business hours
              during office hours. For urgent matters, please call us directly.
            </p>
          </details>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
/* Smooth transitions */
details summary::-webkit-details-marker {
  display: none;
}

/* Floating shapes animation */
.floating-shapes {
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.shape {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  animation: float 20s infinite;
}

.shape-1 {
  width: 300px;
  height: 300px;
  top: -150px;
  left: -150px;
  animation-delay: 0s;
}

.shape-2 {
  width: 200px;
  height: 200px;
  top: 50%;
  right: -100px;
  animation-delay: 5s;
}

.shape-3 {
  width: 250px;
  height: 250px;
  bottom: -125px;
  left: 50%;
  animation-delay: 10s;
}

@keyframes float {
  0%,
  100% {
    transform: translate(0, 0) rotate(0deg);
  }
  33% {
    transform: translate(30px, -30px) rotate(120deg);
  }
  66% {
    transform: translate(-20px, 20px) rotate(240deg);
  }
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

@keyframes fadeInLeft {
  from {
    opacity: 0;
    transform: translateX(-30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeInRight {
  from {
    opacity: 0;
    transform: translateX(30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes bounceSlow {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.animate-fade-in-up {
  animation: fadeInUp 0.8s ease-out forwards;
}

.animate-fade-in-left {
  animation: fadeInLeft 0.8s ease-out forwards;
}

.animate-fade-in-right {
  animation: fadeInRight 0.8s ease-out forwards;
}

.animate-bounce-slow {
  animation: bounceSlow 2s ease-in-out infinite;
}
</style>
