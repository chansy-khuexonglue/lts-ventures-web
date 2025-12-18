<script setup lang="ts">
useHead({
  meta: [{ name: "viewport", content: "width=device-width, initial-scale=1" }],
  link: [
    { rel: "icon", href: "/favicon.ico" },
    { rel: "preconnect", href: "https://fonts.googleapis.com" },
    { rel: "preconnect", href: "https://fonts.gstatic.com", crossorigin: "" },
    {
      rel: "stylesheet",
      href: "https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap",
    },
  ],
  htmlAttrs: {
    lang: "en",
  },
});

const title = "LTS Venture - Innovating Tomorrow, Today";
const description =
  "Leading the future of technology and innovation. We deliver cutting-edge solutions that transform businesses and empower people worldwide.";

useSeoMeta({
  title,
  description,
  ogTitle: title,
  ogDescription: description,
  ogImage: "/og-image.png",
});
</script>

<template>
  <UApp>
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </UApp>
</template>

<style>
:root {
  --font-inter: "Inter", -apple-system, BlinkMacSystemFont, sans-serif;
  --font-jakarta: "Plus Jakarta Sans", sans-serif;
}

body {
  font-family: var(--font-inter);
}
</style>
