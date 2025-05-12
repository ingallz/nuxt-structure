<template>
  <div class="flex h-screen flex-col items-center justify-center">
    <nuxt-img
      draggable="false"
      src="/assets/images/hero-gradient.svg"
      class="absolute right-0 top-0 hidden select-none overflow-hidden blur-lg lg:block"
      alt=""
      width="1269"
      height="724"
    />
    <nuxt-img
      draggable="false"
      src="/assets/images/hero-gradient-tablet.svg"
      alt=""
      class="absolute right-0 top-0 hidden w-full select-none overflow-hidden blur-md sm:block lg:hidden"
      width="924"
      height="653"
    />
    <nuxt-img
      draggable="false"
      src="/assets/images/hero-gradient-mobile.svg"
      class="absolute inset-x-0 top-0 w-full select-none overflow-hidden object-cover blur-md sm:hidden"
      alt=""
      width="375"
      height="494"
    />
    <div class="z-20 flex flex-col gap-3">
      <h1 class="z-10 text-3xl font-semibold md:text-5xl">
        <span class="text-primary">Nuxt 3</span> +
        <span class="text-cyan-400">Tailwind CSS</span>
      </h1>
      <nuxt-link
        to="https://github.com/barbecue/nuxt-structure#readme"
        class="rounded bg-gradient-to-r from-primary to-cyan-500 px-4 py-2 font-semibold text-background transition duration-300 hover:drop-shadow-primary"
      >
        Get Started
      </nuxt-link>
      <span class="text-sm"
        >made by <nuxt-link to="https://github.com/barbecue" class="text-primary">@barbecue</nuxt-link> with
        <Icon name="material-symbols:favorite-rounded" class="h-4 w-4 text-primary"
      /></span>
      
      <!-- Enhanced Navigation Section -->
      <div class="mt-12 w-full max-w-md">
        <h2 class="mb-5 flex items-center gap-2 text-center text-xl font-semibold text-white">
          <div class="h-px flex-1 bg-gradient-to-r from-transparent to-gray-700"></div>
          <span class="flex items-center gap-2">
            <Icon name="ph:compass-duotone" class="h-5 w-5 text-primary" />
            Demo Pages
          </span>
          <div class="h-px flex-1 bg-gradient-to-l from-transparent to-gray-700"></div>
        </h2>
        
        <div class="grid grid-cols-1 gap-3 sm:grid-cols-2">
          <nuxt-link
            v-for="page in pages"
            :key="page.path"
            :to="page.path"
            class="group relative overflow-hidden rounded-xl border border-gray-800 bg-gray-900/70 p-4 backdrop-blur-sm transition-all duration-300 hover:border-primary/50 hover:shadow-lg hover:shadow-primary/10"
          >
            <div class="absolute -right-8 -top-8 h-16 w-16 rounded-full bg-gradient-to-br from-primary/20 to-cyan-500/20 blur-xl transition-all duration-500 group-hover:bg-gradient-to-br group-hover:from-primary/30 group-hover:to-cyan-500/30 group-hover:blur-2xl"></div>
            
            <div class="flex items-center gap-3">
              <div class="flex h-10 w-10 items-center justify-center rounded-lg bg-gray-800 text-primary transition-all duration-300 group-hover:bg-primary/10 group-hover:text-primary">
                <Icon v-if="page.icon" :name="page.icon" class="h-6 w-6" />
              </div>
              <div>
                <h3 class="font-medium text-white">{{ page.title }}</h3>
                <p class="text-xs text-gray-400">{{ page.description }}</p>
              </div>
              <div class="ml-auto">
                <Icon name="heroicons:arrow-right" class="h-4 w-4 text-gray-500 transition-all duration-300 group-hover:translate-x-1 group-hover:text-primary" />
              </div>
            </div>
          </nuxt-link>
          
          <!-- Add New Page Card (placeholder for future pages) -->
          <div class="group relative flex cursor-default items-center justify-center overflow-hidden rounded-xl border border-dashed border-gray-800 bg-gray-900/30 p-6 text-center backdrop-blur-sm">
            <p class="text-sm text-gray-500">More demos coming soon...</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
// Enhanced list of pages for navigation
const pages = [
  {
    title: 'Lifecycle Hooks',
    description: 'Learn the differences between lifecycle hooks',
    path: '/lifecycle-hooks',
    icon: 'mdi:lifecycle',
  },
  {
    title: 'Vue Fundamentals',
    description: 'Core Vue features and patterns',
    path: '/vue-fundamentals',
    icon: 'mdi:vuejs',
  },
  {
    title: 'State Management',
    description: 'Vuex and Pinia for state management',
    path: '/state-management',
    icon: 'mdi:database',
  },
  // Add more pages here as they are created
];
</script>

<style>
/* Add subtle animation for card hover effects */
@keyframes pulse {
  0%, 100% { opacity: 0.8; }
  50% { opacity: 1; }
}
</style>
