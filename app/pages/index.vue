<script setup lang="ts">
import { ref, onMounted } from "vue";

// SEO
const title = "LTS Venture - Empowering Communities Through Innovation";
const description =
  "Leading microfinance and community development organization transforming lives through village banking, sustainable growth, and innovative financial solutions.";

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
  hero: false,
  stats: false,
  about: false,
  services: false,
  team: false,
  projects: false,
  testimonials: false,
  cta: false,
});

// Sliding text animation
const animatedWords = ["Village", "Digital", "Micro-"];
const currentWordIndex = ref(0);
const currentWord = ref(animatedWords[0]);

// Stats counter animation
const stats = ref([
  {
    value: 0,
    target: 10000,
    label: "Transactions / Day",
    suffix: "",
    icon: "i-lucide-users",
  },
  {
    value: 0,
    target: 924,
    label: "Villages",
    suffix: "",
    icon: "i-lucide-map-pin",
  },
  {
    value: 0,
    target: 25,
    label: "Projects",
    suffix: "+",
    icon: "i-lucide-trending-up",
  },
  {
    value: 0,
    target: 5,
    label: "Years Experience",
    suffix: "+",
    icon: "i-lucide-award",
  },
]);

const services = [
  {
    icon: "i-lucide-piggy-bank",
    title: "Village Banking",
    description:
      "Empowering rural communities with accessible microfinance solutions and financial literacy programs.",
    color: "emerald",
  },
  {
    icon: "i-lucide-sprout",
    title: "LTS Growth",
    description:
      "Sustainable development initiatives that create lasting economic opportunities for communities.",
    color: "blue",
  },
  {
    icon: "i-lucide-brain",
    title: "AI Loan Decisioning",
    description:
      "Advanced credit scoring and automated loan processing powered by artificial intelligence.",
    color: "purple",
  },
  {
    icon: "i-lucide-graduation-cap",
    title: "Training Programs",
    description:
      "Comprehensive financial education and entrepreneurship training for community members.",
    color: "red",
  },
  {
    icon: "i-lucide-heart-handshake",
    title: "Community Projects",
    description:
      "Collaborative initiatives that strengthen social bonds and drive collective prosperity.",
    color: "pink",
  },
  {
    icon: "i-lucide-smartphone",
    title: "Lan Xang Banker",
    description:
      "Digital banking platform bringing modern financial services to underserved communities.",
    color: "cyan",
  },
];

const team = [
  {
    name: "Dr. Sarah Johnson",
    role: "Chief Executive Officer",
    image: "https://i.pravatar.cc/400?img=1",
    bio: "20+ years in microfinance",
  },
  {
    name: "Michael Chen",
    role: "Chief Technology Officer",
    image: "https://i.pravatar.cc/400?img=13",
    bio: "Fintech innovation expert",
  },
  {
    name: "Amara Patel",
    role: "Head of Operations",
    image: "https://i.pravatar.cc/400?img=5",
    bio: "Community development specialist",
  },
  {
    name: "James Williams",
    role: "Chief Financial Officer",
    image: "https://i.pravatar.cc/400?img=12",
    bio: "Strategic finance leader",
  },
];

const testimonials = [
  {
    quote:
      "LTS Venture transformed our village. The microfinance program helped me start my own business and support my family.",
    author: "Bouasone Keomany",
    role: "Small Business Owner",
    avatar: "https://i.pravatar.cc/150?img=30",
    rating: 5,
  },
  {
    quote:
      "The training programs gave me the skills and confidence to manage my finances and plan for the future.",
    author: "Nang Vilayvanh",
    role: "Community Leader",
    avatar: "https://i.pravatar.cc/150?img=32",
    rating: 5,
  },
  {
    quote:
      "Their innovative approach to banking has made financial services accessible to everyone in our community.",
    author: "Khamla Phomvihane",
    role: "Village Chief",
    avatar: "https://i.pravatar.cc/150?img=33",
    rating: 5,
  },
];

const projects = [
  {
    title: "Rural Electrification Initiative",
    description: "Bringing sustainable energy solutions to 50+ villages",
    image:
      "https://images.unsplash.com/photo-1473341304170-971dccb5ac1e?w=800&h=600&fit=crop",
    impact: "5,000+ households",
  },
  {
    title: "Women Entrepreneurship Program",
    description: "Empowering women through business training and microloans",
    image:
      "https://images.unsplash.com/photo-1573164713714-d95e436ab8d6?w=800&h=600&fit=crop",
    impact: "2,500+ women trained",
  },
  {
    title: "Agricultural Innovation Hub",
    description: "Modern farming techniques and market access for farmers",
    image:
      "https://images.unsplash.com/photo-1625246333195-78d9c38ad449?w=800&h=600&fit=crop",
    impact: "1,200+ farmers",
  },
];

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

          // Animate stats counter
          if (target === "stats") {
            animateStats();
          }
        }
      }
    });
  }, observerOptions);

  // Observe all sections
  document.querySelectorAll("[data-section]").forEach((section) => {
    observer.observe(section);
  });

  // Hero is visible immediately
  isVisible.value.hero = true;

  // Start word animation
  setInterval(() => {
    currentWordIndex.value =
      (currentWordIndex.value + 1) % animatedWords.length;
    currentWord.value = animatedWords[currentWordIndex.value];
  }, 3000); // Change word every 3 seconds
});

function animateStats() {
  stats.value.forEach((stat, index) => {
    const duration = 2000;
    const steps = 60;
    const increment = stat.target / steps;
    let current = 0;

    const timer = setInterval(() => {
      current += increment;
      if (current >= stat.target) {
        stat.value = stat.target;
        clearInterval(timer);
      } else {
        stat.value = Math.floor(current);
      }
    }, duration / steps);
  });
}

function scrollToSection(id: string) {
  const element = document.getElementById(id);
  if (element) {
    element.scrollIntoView({ behavior: "smooth" });
  }
}
</script>

<template>
  <div class="min-h-screen bg-gray-50 dark:bg-gray-950">
    <!-- Hero Section -->
    <section
      id="hero"
      data-section="hero"
      class="relative min-h-screen flex items-center justify-center overflow-hidden"
    >
      <!-- Background Image with Overlay -->
      <div class="absolute inset-0 overflow-hidden">
        <!-- Background Image -->
        <div
          class="absolute inset-0 bg-cover bg-center bg-no-repeat"
          style="
            background-image: url('https://i.pinimg.com/1200x/bc/5e/07/bc5e0705b45261d8c5a01ba59030591c.jpg');
          "
        />
        <!-- Dark Overlay for text readability -->
        <div
          class="absolute inset-0 bg-gradient-to-br from-blue-900/70 via-purple-900/60 to-pink-900/70"
        />
        <!-- Pattern Overlay -->
        <div class="absolute inset-0 hero-pattern opacity-10" />
        <!-- Floating Shapes -->
        <div class="floating-shapes">
          <div class="shape shape-1" />
          <div class="shape shape-2" />
          <div class="shape shape-3" />
        </div>
      </div>

      <!-- Content -->
      <div class="relative z-10 container mx-auto px-4 py-20 text-center">
        <div
          class="hero-content"
          :class="{ 'animate-fade-in-up': isVisible.hero }"
        >
          <h1
            class="text-5xl md:text-7xl font-bold text-white mb-6 leading-tight"
          >
            Empowering Communities<br />
            <span class="inline-flex items-center justify-center gap-3">
              <span
                class="inline-block relative w-64 md:w-96 h-16 md:h-20 overflow-hidden"
              >
                <TransitionGroup name="slide-up" tag="div">
                  <span
                    :key="currentWord"
                    class="absolute inset-0 flex items-center justify-center text-transparent bg-clip-text bg-gradient-to-r from-yellow-300 to-orange-300 font-bold"
                  >
                    {{ currentWord }}
                  </span>
                </TransitionGroup>
              </span>
              <span
                class="text-transparent bg-clip-text bg-gradient-to-r from-yellow-300 to-orange-300"
              >
                Banking
              </span>
            </span>
          </h1>
          <p class="text-xl md:text-2xl text-white/90 mb-8 max-w-3xl mx-auto">
            Transforming lives through sustainable microfinance, community
            development, and cutting-edge financial technology
          </p>
          <div class="flex flex-wrap gap-4 justify-center">
            <UButton
              size="xl"
              color="neutral"
              variant="solid"
              icon="i-lucide-rocket"
              @click="scrollToSection('services')"
            >
              Explore Our Services
            </UButton>
            <UButton
              size="xl"
              color="neutral"
              variant="outline"
              icon="i-lucide-phone"
              to="/contact-us"
            >
              Get in Touch
            </UButton>
          </div>
        </div>

        <!-- Scroll Indicator -->
        <!-- <div class="absolute bottom-4 left-1/2 -translate-x-1/2 animate-bounce">
          <UIcon name="i-lucide-chevron-down" class="w-8 h-8 text-white/70" />
        </div> -->
      </div>
    </section>

    <!-- Stats Section -->
    <section
      id="stats"
      data-section="stats"
      class="py-20 bg-white dark:bg-gray-900 relative overflow-hidden"
    >
      <div
        class="absolute inset-0 bg-gradient-to-r from-blue-50 to-purple-50 dark:from-gray-800 dark:to-gray-900 opacity-50"
      />
      <div class="container mx-auto px-4 relative z-10">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
          <div
            v-for="(stat, index) in stats"
            :key="index"
            class="text-center p-8 rounded-2xl bg-white dark:bg-gray-800 shadow-lg hover:shadow-xl transition-all duration-300 hover:-translate-y-2"
            :class="{ 'animate-fade-in-up': isVisible.stats }"
            :style="{ animationDelay: `${index * 100}ms` }"
          >
            <div
              class="inline-flex items-center justify-center w-16 h-16 rounded-full bg-gradient-to-br from-blue-500 to-blue-600 mb-4"
            >
              <UIcon :name="stat.icon" class="w-8 h-8 text-white" />
            </div>
            <div class="text-4xl font-bold text-gray-900 dark:text-white mb-2">
              {{ stat.value }}{{ stat.suffix }}
            </div>
            <div class="text-gray-600 dark:text-gray-400 font-medium">
              {{ stat.label }}
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section
      id="about"
      data-section="about"
      class="py-20 bg-gray-50 dark:bg-gray-950"
    >
      <div class="container mx-auto px-4">
        <div class="grid md:grid-cols-2 gap-12 items-center">
          <div
            class="space-y-6"
            :class="{ 'animate-fade-in-left': isVisible.about }"
          >
            <div
              class="inline-block px-4 py-2 bg-blue-100 dark:bg-blue-900/30 text-blue-600 dark:text-blue-400 rounded-full text-sm font-semibold"
            >
              About LTS Venture
            </div>
            <h2
              class="text-4xl md:text-5xl font-bold text-gray-900 dark:text-white"
            >
              Building Brighter Futures Together
            </h2>
            <p class="text-lg text-gray-600 dark:text-gray-400 leading-relaxed">
              For over 50 years, LTS Venture has been at the forefront of
              community development and microfinance innovation. We believe that
              everyone deserves access to financial services and the opportunity
              to build a better future.
            </p>
            <p class="text-lg text-gray-600 dark:text-gray-400 leading-relaxed">
              Our integrated approach combines traditional village banking with
              cutting-edge technology, creating sustainable solutions that
              empower communities and transform lives across the region.
            </p>
            <div class="flex gap-4">
              <UButton
                size="lg"
                color="primary"
                icon="i-lucide-arrow-right"
                trailing
              >
                Learn More About Us
              </UButton>
            </div>
          </div>
          <div
            class="relative"
            :class="{ 'animate-fade-in-right': isVisible.about }"
          >
            <div class="relative rounded-2xl overflow-hidden shadow-2xl">
              <img
                src="https://images.unsplash.com/photo-1559027615-cd4628902d4a?w=800&h=600&fit=crop"
                alt="Community gathering"
                class="w-full h-auto"
              />
              <div
                class="absolute inset-0 bg-gradient-to-t from-black/50 to-transparent"
              />
            </div>
            <!-- Floating card -->
            <div
              class="absolute -bottom-6 -left-6 bg-white dark:bg-gray-800 p-6 rounded-xl shadow-xl max-w-xs"
            >
              <div class="flex items-center gap-4">
                <div
                  class="w-12 h-12 rounded-full bg-green-500 flex items-center justify-center"
                >
                  <UIcon name="i-lucide-check" class="w-6 h-6 text-white" />
                </div>
                <div>
                  <div class="font-bold text-gray-900 dark:text-white">
                    Trusted Partner
                  </div>
                  <div class="text-sm text-gray-600 dark:text-gray-400">
                    Since 1973
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Services Section -->
    <section
      id="services"
      data-section="services"
      class="py-20 bg-white dark:bg-gray-900"
    >
      <div class="container mx-auto px-4">
        <div class="text-center mb-16">
          <div
            class="inline-block px-4 py-2 bg-purple-100 dark:bg-purple-900/30 text-purple-600 dark:text-purple-400 rounded-full text-sm font-semibold mb-4"
          >
            What We Do
          </div>
          <h2
            class="text-4xl md:text-5xl font-bold text-gray-900 dark:text-white mb-4"
          >
            Comprehensive Solutions for Communities
          </h2>
          <p class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">
            From traditional village banking to AI-powered financial services,
            we offer a complete ecosystem of solutions
          </p>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div
            v-for="(service, index) in services"
            :key="index"
            class="group relative p-8 rounded-2xl bg-gradient-to-br from-gray-50 to-gray-100 dark:from-gray-800 dark:to-gray-900 hover:shadow-2xl transition-all duration-300 hover:-translate-y-2 overflow-hidden"
            :class="{ 'animate-fade-in-up': isVisible.services }"
            :style="{ animationDelay: `${index * 100}ms` }"
          >
            <!-- Gradient overlay on hover -->
            <div
              class="absolute inset-0 bg-gradient-to-br opacity-0 group-hover:opacity-10 transition-opacity duration-300"
              :class="`from-${service.color}-400 to-${service.color}-600`"
            />

            <div class="relative z-10">
              <div
                class="inline-flex items-center justify-center w-16 h-16 rounded-xl mb-6 bg-gradient-to-br transition-transform duration-300 group-hover:scale-110"
                :class="`from-${service.color}-400 to-${service.color}-600`"
              >
                <UIcon :name="service.icon" class="w-8 h-8 text-white" />
              </div>
              <h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-3">
                {{ service.title }}
              </h3>
              <p class="text-gray-600 dark:text-gray-400 leading-relaxed mb-4">
                {{ service.description }}
              </p>
              <UButton
                variant="ghost"
                color="neutral"
                icon="i-lucide-arrow-right"
                trailing
                class="group-hover:translate-x-2 transition-transform"
              >
                Learn More
              </UButton>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section
      id="projects"
      data-section="projects"
      class="py-20 bg-gray-50 dark:bg-gray-950"
    >
      <div class="container mx-auto px-4">
        <div class="text-center mb-16">
          <div
            class="inline-block px-4 py-2 bg-green-100 dark:bg-green-900/30 text-green-600 dark:text-green-400 rounded-full text-sm font-semibold mb-4"
          >
            Our Impact
          </div>
          <h2
            class="text-4xl md:text-5xl font-bold text-gray-900 dark:text-white mb-4"
          >
            Projects That Transform Lives
          </h2>
          <p class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">
            Real initiatives creating lasting change in communities across the
            region
          </p>
        </div>

        <div class="grid md:grid-cols-3 gap-8">
          <div
            v-for="(project, index) in projects"
            :key="index"
            class="group relative rounded-2xl overflow-hidden shadow-lg hover:shadow-2xl transition-all duration-300"
            :class="{ 'animate-fade-in-up': isVisible.projects }"
            :style="{ animationDelay: `${index * 100}ms` }"
          >
            <div class="relative h-64 overflow-hidden">
              <img
                :src="project.image"
                :alt="project.title"
                class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110"
              />
              <div
                class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/40 to-transparent"
              />

              <!-- Impact badge -->
              <div
                class="absolute top-4 right-4 bg-white/90 dark:bg-gray-900/90 backdrop-blur-sm px-4 py-2 rounded-full"
              >
                <div class="text-sm font-bold text-gray-900 dark:text-white">
                  {{ project.impact }}
                </div>
              </div>
            </div>

            <div class="absolute bottom-0 left-0 right-0 p-6 text-white">
              <h3 class="text-2xl font-bold mb-2">
                {{ project.title }}
              </h3>
              <p class="text-white/90 mb-4">
                {{ project.description }}
              </p>
              <UButton
                variant="solid"
                color="neutral"
                size="sm"
                icon="i-lucide-external-link"
                trailing
              >
                View Project
              </UButton>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Team Section -->
    <section
      id="team"
      data-section="team"
      class="py-20 bg-white dark:bg-gray-900"
    >
      <div class="container mx-auto px-4">
        <div class="text-center mb-16">
          <div
            class="inline-block px-4 py-2 bg-orange-100 dark:bg-orange-900/30 text-orange-600 dark:text-orange-400 rounded-full text-sm font-semibold mb-4"
          >
            Our Team
          </div>
          <h2
            class="text-4xl md:text-5xl font-bold text-gray-900 dark:text-white mb-4"
          >
            Led by Visionary Leaders
          </h2>
          <p class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">
            Experienced professionals dedicated to creating positive social
            impact
          </p>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8">
          <div
            v-for="(member, index) in team"
            :key="index"
            class="group text-center"
            :class="{ 'animate-fade-in-up': isVisible.team }"
            :style="{ animationDelay: `${index * 100}ms` }"
          >
            <div class="relative mb-6 inline-block">
              <div
                class="relative w-48 h-48 mx-auto rounded-2xl overflow-hidden shadow-lg group-hover:shadow-2xl transition-all duration-300"
              >
                <img
                  :src="member.image"
                  :alt="member.name"
                  class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110"
                />
                <div
                  class="absolute inset-0 bg-gradient-to-t from-black/60 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300"
                />
              </div>
              <!-- Social links on hover -->
              <div
                class="absolute bottom-4 left-1/2 -translate-x-1/2 flex gap-2 opacity-0 group-hover:opacity-100 transition-opacity duration-300"
              >
                <UButton
                  icon="i-lucide-linkedin"
                  size="sm"
                  color="neutral"
                  variant="solid"
                  square
                />
                <UButton
                  icon="i-lucide-mail"
                  size="sm"
                  color="neutral"
                  variant="solid"
                  square
                />
              </div>
            </div>
            <h3 class="text-xl font-bold text-gray-900 dark:text-white mb-1">
              {{ member.name }}
            </h3>
            <p class="text-blue-600 dark:text-blue-400 font-medium mb-2">
              {{ member.role }}
            </p>
            <p class="text-sm text-gray-600 dark:text-gray-400">
              {{ member.bio }}
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Testimonials Section -->
    <section
      id="testimonials"
      data-section="testimonials"
      class="py-20 bg-gradient-to-br from-blue-600 to-purple-600 relative overflow-hidden"
    >
      <div class="absolute inset-0 hero-pattern opacity-10" />
      <div class="container mx-auto px-4 relative z-10">
        <div class="text-center mb-16">
          <div
            class="inline-block px-4 py-2 bg-white/20 backdrop-blur-sm text-white rounded-full text-sm font-semibold mb-4"
          >
            Testimonials
          </div>
          <h2 class="text-4xl md:text-5xl font-bold text-white mb-4">
            Stories from Our Community
          </h2>
          <p class="text-lg text-white/90 max-w-2xl mx-auto">
            Hear from the people whose lives have been transformed by our
            programs
          </p>
        </div>

        <div class="grid md:grid-cols-3 gap-8">
          <div
            v-for="(testimonial, index) in testimonials"
            :key="index"
            class="bg-white dark:bg-gray-800 p-8 rounded-2xl shadow-xl"
            :class="{ 'animate-fade-in-up': isVisible.testimonials }"
            :style="{ animationDelay: `${index * 100}ms` }"
          >
            <!-- Rating stars -->
            <div class="flex gap-1 mb-4">
              <UIcon
                v-for="star in testimonial.rating"
                :key="star"
                name="i-lucide-star"
                class="w-5 h-5 text-yellow-400 fill-yellow-400"
              />
            </div>

            <p
              class="text-gray-700 dark:text-gray-300 mb-6 italic leading-relaxed"
            >
              "{{ testimonial.quote }}"
            </p>

            <div class="flex items-center gap-4">
              <img
                :src="testimonial.avatar"
                :alt="testimonial.author"
                class="w-12 h-12 rounded-full"
              />
              <div>
                <div class="font-bold text-gray-900 dark:text-white">
                  {{ testimonial.author }}
                </div>
                <div class="text-sm text-gray-600 dark:text-gray-400">
                  {{ testimonial.role }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section
      id="cta"
      data-section="cta"
      class="py-20 bg-gray-900 dark:bg-black relative overflow-hidden"
    >
      <div
        class="absolute inset-0 bg-gradient-to-r from-blue-600/20 to-purple-600/20"
      />
      <div class="container mx-auto px-4 relative z-10 text-center">
        <div
          class="max-w-3xl mx-auto"
          :class="{ 'animate-fade-in-up': isVisible.cta }"
        >
          <h2 class="text-4xl md:text-5xl font-bold text-white mb-6">
            Ready to Make a Difference?
          </h2>
          <p class="text-xl text-gray-300 mb-8">
            Join us in our mission to empower communities and create sustainable
            change. Whether you're looking for financial services or want to
            partner with us, we're here to help.
          </p>
          <div class="flex flex-wrap gap-4 justify-center">
            <UButton
              size="xl"
              color="primary"
              icon="i-lucide-rocket"
              to="/contact-us"
            >
              Get Started Today
            </UButton>
            <UButton
              size="xl"
              color="neutral"
              variant="outline"
              icon="i-lucide-calendar"
            >
              Schedule a Consultation
            </UButton>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-950 text-gray-400 py-12">
      <div class="container mx-auto px-4">
        <div class="grid md:grid-cols-4 gap-8 mb-8">
          <div>
            <img src="@/assets/logo.png" alt="LTS Venture" class="w-32 mb-4" />
            <p class="text-sm">
              Empowering communities through innovation and sustainable
              development since 1973.
            </p>
          </div>
          <div>
            <h4 class="text-white font-bold mb-4">Quick Links</h4>
            <ul class="space-y-2 text-sm">
              <li>
                <a href="#" class="hover:text-white transition-colors"
                  >About Us</a
                >
              </li>
              <li>
                <a href="#" class="hover:text-white transition-colors"
                  >Our Services</a
                >
              </li>
              <li>
                <a href="#" class="hover:text-white transition-colors"
                  >Projects</a
                >
              </li>
              <li>
                <a href="#" class="hover:text-white transition-colors"
                  >Careers</a
                >
              </li>
            </ul>
          </div>
          <div>
            <h4 class="text-white font-bold mb-4">Services</h4>
            <ul class="space-y-2 text-sm">
              <li>
                <a href="#" class="hover:text-white transition-colors"
                  >Village Banking</a
                >
              </li>
              <li>
                <a href="#" class="hover:text-white transition-colors"
                  >LTS Growth</a
                >
              </li>
              <li>
                <a href="#" class="hover:text-white transition-colors"
                  >Lan Xang Banker</a
                >
              </li>
              <li>
                <a href="#" class="hover:text-white transition-colors"
                  >Training Programs</a
                >
              </li>
            </ul>
          </div>
          <div>
            <h4 class="text-white font-bold mb-4">Connect</h4>
            <div class="flex gap-3 mb-4">
              <UButton
                icon="i-lucide-facebook"
                size="sm"
                color="neutral"
                variant="soft"
                square
              />
              <UButton
                icon="i-lucide-twitter"
                size="sm"
                color="neutral"
                variant="soft"
                square
              />
              <UButton
                icon="i-lucide-linkedin"
                size="sm"
                color="neutral"
                variant="soft"
                square
              />
              <UButton
                icon="i-lucide-instagram"
                size="sm"
                color="neutral"
                variant="soft"
                square
              />
            </div>
            <p class="text-sm">
              <UIcon name="i-lucide-mail" class="inline w-4 h-4" />
              info@ltsventure.com
            </p>
          </div>
        </div>
        <div class="border-t border-gray-800 pt-8 text-center text-sm">
          <p>
            &copy; {{ new Date().getFullYear() }} LTS Venture. All rights
            reserved.
          </p>
        </div>
      </div>
    </footer>
  </div>
</template>

<style scoped>
/* Hero Pattern */
.hero-pattern {
  background-image: radial-gradient(
    circle at 2px 2px,
    rgba(255, 255, 255, 0.15) 1px,
    transparent 0
  );
  background-size: 50px 50px;
}

/* Floating Shapes Animation */
.floating-shapes {
  position: absolute;
  inset: 0;
  overflow: hidden;
}

.shape {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  animation: float 20s infinite ease-in-out;
}

.shape-1 {
  width: 300px;
  height: 300px;
  top: 10%;
  left: 10%;
  animation-delay: 0s;
}

.shape-2 {
  width: 200px;
  height: 200px;
  top: 60%;
  right: 15%;
  animation-delay: 5s;
}

.shape-3 {
  width: 150px;
  height: 150px;
  bottom: 20%;
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

/* Fade In Animations */
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

.animate-fade-in-up {
  animation: fadeInUp 0.8s ease-out forwards;
}

.animate-fade-in-left {
  animation: fadeInLeft 0.8s ease-out forwards;
}

.animate-fade-in-right {
  animation: fadeInRight 0.8s ease-out forwards;
}

/* Smooth scrolling */
html {
  scroll-behavior: smooth;
}

/* Slide-up text animation */
.slide-up-enter-active,
.slide-up-leave-active {
  transition: all 0.6s ease;
}

.slide-up-enter-from {
  opacity: 0;
  transform: translateY(100%);
}

.slide-up-enter-to {
  opacity: 1;
  transform: translateY(0);
}

.slide-up-leave-from {
  opacity: 1;
  transform: translateY(0);
}

.slide-up-leave-to {
  opacity: 0;
  transform: translateY(-100%);
}
</style>
