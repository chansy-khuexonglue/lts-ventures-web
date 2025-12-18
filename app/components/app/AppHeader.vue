<script setup lang="ts">
const isScrolled = ref(false);
const isMobileMenuOpen = ref(false);
const isHeaderVisible = ref(true);
const lastScrollY = ref(0);

const handleScroll = () => {
  const currentScrollY = window.scrollY;

  // Determine if scrolled
  isScrolled.value = currentScrollY > 20;

  // Show/hide header based on scroll direction
  if (currentScrollY > lastScrollY.value && currentScrollY > 100) {
    // Scrolling down & past 100px - hide header
    isHeaderVisible.value = false;
  } else {
    // Scrolling up or at top - show header
    isHeaderVisible.value = true;
  }

  lastScrollY.value = currentScrollY;
};

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value;
  // Prevent body scroll when menu is open
  if (isMobileMenuOpen.value) {
    document.body.style.overflow = "hidden";
  } else {
    document.body.style.overflow = "";
  }
};

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false;
  document.body.style.overflow = "";
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
  handleScroll(); // Check initial state
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
  document.body.style.overflow = ""; // Cleanup
});
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-300 bg-white/95 dark:bg-gray-900/95 backdrop-blur-lg shadow-md"
    :class="{
      'shadow-lg': isScrolled,
      '-translate-y-full': !isHeaderVisible,
      'translate-y-0': isHeaderVisible,
    }"
  >
    <div class="container mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center h-16 md:h-20">
        <!-- Logo Section -->
        <div
          class="flex-shrink-0 transition-transform duration-300 hover:scale-105 z-50"
        >
          <NuxtLink
            to="/"
            class="flex items-center gap-2 md:gap-3 group"
            @click="closeMobileMenu"
          >
            <div class="relative">
              <img
                src="@/assets/logo.png"
                alt="LTS Venture Logo"
                class="h-10 md:h-12 w-auto transition-all duration-300"
              />
              <!-- Glow effect on hover -->
              <div
                class="absolute inset-0 bg-gradient-to-r from-blue-500 to-purple-600 rounded-full blur-xl opacity-0 group-hover:opacity-30 transition-opacity duration-300 -z-10"
              />
            </div>
            <div class="hidden sm:block">
              <div
                class="text-lg md:text-xl font-bold bg-gradient-to-r from-blue-600 to-purple-600 bg-clip-text text-transparent transition-all duration-300"
                :class="{
                  'from-gray-900 to-gray-700 dark:from-white dark:to-gray-300':
                    isScrolled || isMobileMenuOpen,
                }"
              >
                LTS Venture
              </div>
              <div
                class="text-[10px] md:text-xs text-gray-600 dark:text-gray-400 font-medium"
              >
                Empowering Communities
              </div>
            </div>
          </NuxtLink>
        </div>

        <!-- Desktop Navigation Menu - Hidden on mobile/tablet -->
        <nav class="hidden lg:flex items-center">
          <AppMenu :is-mobile="false" />
        </nav>

        <!-- Desktop CTA Button - Hidden on mobile/tablet -->
        <div class="hidden lg:flex items-center gap-4">
          <UButton
            to="/contact-us"
            color="primary"
            size="md"
            icon="i-lucide-phone"
            class="transition-all duration-300 hover:scale-105"
          >
            Contact Us
          </UButton>
        </div>

        <!-- Mobile Menu Button - Shown on mobile/tablet -->
        <div class="lg:hidden z-50">
          <button
            @click="toggleMobileMenu"
            class="p-2.5 rounded-xl transition-all duration-300 shadow-lg border border-gray-200 dark:border-gray-700"
            :class="{
              'bg-white/90 dark:bg-gray-800/90 text-gray-900 dark:text-white hover:bg-white dark:hover:bg-gray-800':
                isScrolled || isMobileMenuOpen,
              'bg-white/20 dark:bg-gray-900/20 backdrop-blur-md text-gray-900 dark:text-white hover:bg-white/30 dark:hover:bg-gray-900/30':
                !isScrolled && !isMobileMenuOpen,
            }"
            aria-label="Toggle menu"
          >
            <!-- Hamburger Icon -->
            <div
              class="w-5 h-5 flex flex-col justify-center items-center gap-1.5"
            >
              <span
                class="w-5 h-0.5 bg-current transition-all duration-300 origin-center"
                :class="{
                  'rotate-45 translate-y-2': isMobileMenuOpen,
                }"
              />
              <span
                class="w-5 h-0.5 bg-current transition-all duration-300"
                :class="{
                  'opacity-0 scale-0': isMobileMenuOpen,
                }"
              />
              <span
                class="w-5 h-0.5 bg-current transition-all duration-300 origin-center"
                :class="{
                  '-rotate-45 -translate-y-2': isMobileMenuOpen,
                }"
              />
            </div>
          </button>
        </div>
      </div>
    </div>

    <!-- Bottom border with gradient -->
    <div
      class="h-[2px] bg-gradient-to-r from-transparent via-blue-500 to-transparent transition-opacity duration-300"
      :class="{
        'opacity-100': isScrolled,
        'opacity-0': !isScrolled && !isMobileMenuOpen,
      }"
    />
  </header>

  <!-- Mobile Menu Overlay -->
  <Transition
    enter-active-class="transition-opacity duration-300"
    enter-from-class="opacity-0"
    enter-to-class="opacity-100"
    leave-active-class="transition-opacity duration-300"
    leave-from-class="opacity-100"
    leave-to-class="opacity-0"
  >
    <div
      v-if="isMobileMenuOpen"
      class="fixed inset-0 bg-black/50 backdrop-blur-sm z-40 lg:hidden"
      @click="closeMobileMenu"
    />
  </Transition>

  <!-- Mobile Menu Drawer -->
  <Transition
    enter-active-class="transition-transform duration-300 ease-out"
    enter-from-class="translate-x-full"
    enter-to-class="translate-x-0"
    leave-active-class="transition-transform duration-300 ease-in"
    leave-from-class="translate-x-0"
    leave-to-class="translate-x-full"
  >
    <div
      v-if="isMobileMenuOpen"
      class="fixed top-16 md:top-20 right-0 bottom-0 w-full sm:w-80 bg-white dark:bg-gray-900 shadow-2xl z-40 lg:hidden overflow-y-auto"
    >
      <div class="p-6 space-y-6">
        <!-- Mobile Navigation -->
        <nav class="space-y-4">
          <div
            class="text-sm font-semibold text-gray-500 dark:text-gray-400 uppercase tracking-wider mb-4"
          >
            Navigation
          </div>

          <!-- Use AppMenu component for mobile -->
          <div @click="closeMobileMenu">
            <AppMenu :is-mobile="true" />
          </div>
        </nav>

        <!-- Mobile CTA -->
        <div class="pt-6 border-t border-gray-200 dark:border-gray-800">
          <UButton
            to="/contact-us"
            color="primary"
            variant="solid"
            size="lg"
            icon="i-lucide-phone"
            block
            @click="closeMobileMenu"
          >
            Get in Touch
          </UButton>
        </div>

        <!-- Social Links (Optional) -->
        <div class="pt-6 border-t border-gray-200 dark:border-gray-800">
          <div
            class="text-sm font-semibold text-gray-500 dark:text-gray-400 uppercase tracking-wider mb-4"
          >
            Connect With Us
          </div>
          <div class="flex gap-3">
            <UButton
              icon="i-lucide-facebook"
              size="lg"
              color="neutral"
              variant="soft"
              square
            />
            <UButton
              icon="i-lucide-twitter"
              size="lg"
              color="neutral"
              variant="soft"
              square
            />
            <UButton
              icon="i-lucide-linkedin"
              size="lg"
              color="neutral"
              variant="soft"
              square
            />
            <UButton
              icon="i-lucide-instagram"
              size="lg"
              color="neutral"
              variant="soft"
              square
            />
          </div>
        </div>
      </div>
    </div>
  </Transition>
</template>

<style scoped>
/* Smooth backdrop blur support */
@supports (backdrop-filter: blur(10px)) {
  header {
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
  }
}

/* Enhanced shadow on scroll */
header.shadow-lg {
  box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.1);
}

/* Dark mode adjustments */
@media (prefers-color-scheme: dark) {
  header.shadow-lg {
    box-shadow: 0 10px 30px -10px rgba(0, 0, 0, 0.3);
  }
}

/* Smooth scrolling for mobile menu */
.overflow-y-auto {
  -webkit-overflow-scrolling: touch;
}
</style>
