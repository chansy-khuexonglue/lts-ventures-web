<script setup lang="ts">
const currentYear = new Date().getFullYear();

const quickLinks = [
  { label: "About Us", to: "/about-us" },
  { label: "What We Do", to: "/what-we-do" },
  { label: "Lan Xang Banker", to: "/lan-xang-banker" },
  { label: "Careers", to: "/career" },
];

const services = [
  { label: "Village Banking", to: "/what-we-do#village-banking" },
  { label: "Digital Banking", to: "/lan-xang-banker" },
  { label: "Micro-Finance", to: "/what-we-do#microfinance" },
  { label: "Training Programs", to: "/what-we-do#training" },
];

const socialLinks = [
  { icon: "i-lucide-facebook", url: "#", label: "Facebook" },
  { icon: "i-lucide-twitter", url: "#", label: "Twitter" },
  { icon: "i-lucide-linkedin", url: "#", label: "LinkedIn" },
  { icon: "i-lucide-instagram", url: "#", label: "Instagram" },
];
</script>

<template>
  <footer class="bg-gray-950 text-gray-400">
    <div class="container mx-auto px-4">
      <!-- Main Footer Content -->
      <div class="py-12 md:py-16">
        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-8 md:gap-12">
          <!-- Company Info -->
          <div class="lg:col-span-1">
            <img
              src="@/assets/logo.png"
              alt="LTS Venture"
              class="w-32 mb-4 brightness-0 invert opacity-90"
            />
            <p class="text-sm leading-relaxed mb-4">
              Empowering communities through innovation and sustainable
              development since 2022.
            </p>
            <div class="flex items-center gap-2 text-sm">
              <UIcon name="i-lucide-mail" class="w-4 h-4 text-blue-400" />
              <a
                href="mailto:info@ltsventure.la"
                class="hover:text-white transition-colors"
              >
                info@ltsventure.la
              </a>
            </div>
          </div>

          <!-- Quick Links -->
          <div>
            <h4 class="text-white font-bold mb-4 text-lg">Quick Links</h4>
            <ul class="space-y-3">
              <li v-for="link in quickLinks" :key="link.to">
                <NuxtLink
                  :to="link.to"
                  class="text-sm hover:text-white hover:translate-x-1 inline-block transition-all duration-200"
                >
                  {{ link.label }}
                </NuxtLink>
              </li>
            </ul>
          </div>

          <!-- Services -->
          <div>
            <h4 class="text-white font-bold mb-4 text-lg">Services</h4>
            <ul class="space-y-3">
              <li v-for="service in services" :key="service.to">
                <NuxtLink
                  :to="service.to"
                  class="text-sm hover:text-white hover:translate-x-1 inline-block transition-all duration-200"
                >
                  {{ service.label }}
                </NuxtLink>
              </li>
            </ul>
          </div>

          <!-- Connect -->
          <div>
            <h4 class="text-white font-bold mb-4 text-lg">Connect With Us</h4>
            <div class="flex gap-3 mb-6">
              <a
                v-for="social in socialLinks"
                :key="social.label"
                :href="social.url"
                :aria-label="social.label"
                class="w-10 h-10 rounded-lg bg-gray-800 hover:bg-gray-700 flex items-center justify-center transition-all hover:scale-110"
              >
                <UIcon :name="social.icon" class="w-5 h-5" />
              </a>
            </div>
            <div class="space-y-2 text-sm">
              <div class="flex items-center gap-2">
                <UIcon name="i-lucide-phone" class="w-4 h-4 text-green-400" />
                <a
                  href="tel:+85621123456"
                  class="hover:text-white transition-colors"
                >
                  +856 21 123 456
                </a>
              </div>
              <div class="flex items-center gap-2">
                <UIcon name="i-lucide-map-pin" class="w-4 h-4 text-red-400" />
                <span>Vientiane, Laos</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Bottom Bar -->
      <div class="border-t border-gray-800 py-6">
        <div
          class="flex flex-col md:flex-row justify-between items-center gap-4"
        >
          <p class="text-sm text-center md:text-left">
            &copy; {{ currentYear }} LTS Venture. All rights reserved.
          </p>
          <div class="flex gap-6 text-sm">
            <NuxtLink to="/privacy" class="hover:text-white transition-colors">
              Privacy Policy
            </NuxtLink>
            <NuxtLink to="/terms" class="hover:text-white transition-colors">
              Terms of Service
            </NuxtLink>
            <NuxtLink
              to="/contact-us"
              class="hover:text-white transition-colors"
            >
              Contact
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
/* Add any footer-specific styles here */
</style>
