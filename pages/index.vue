<template>
  <div class="min-h-screen flex flex-col">
    <!-- Hero Section with Background -->
    <section class="relative flex items-center justify-center min-h-screen overflow-hidden">
      <!-- Background Images (keep existing) -->
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
      
      <!-- Hero Content -->
      <div class="container mx-auto px-4 z-20 text-center">
        <div class="max-w-3xl mx-auto">
          <div class="inline-block mb-4 px-3 py-1 rounded-full bg-primary/10 border border-primary/20">
            <span class="text-sm font-medium text-primary">Educational Project</span>
          </div>
          
          <h1 class="text-4xl md:text-6xl font-bold mb-6">
            <span class="text-primary">Nuxt 3</span> +
            <span class="text-cyan-400">Tailwind CSS</span>
          </h1>
          
          <p class="text-gray-400 text-lg mb-8 max-w-2xl mx-auto">
            A comprehensive educational platform demonstrating best practices, patterns, and techniques for building modern applications with Nuxt 3.
          </p>
          
          <div class="flex flex-wrap justify-center gap-4 mb-8">
            <nuxt-link
              to="https://github.com/ingallz/nuxt-structure#readme"
              class="rounded-full bg-gradient-to-r from-primary to-cyan-500 px-6 py-3 font-semibold text-background transition duration-300 hover:shadow-lg hover:shadow-primary/20"
            >
              Get Started
            </nuxt-link>
            <a 
              href="#features" 
              class="rounded-full bg-gray-800 border border-gray-700 px-6 py-3 font-semibold text-white transition duration-300 hover:bg-gray-700"
            >
              Explore Features
            </a>
          </div>
          
          <div class="flex items-center justify-center text-sm text-gray-400">
            <span>made by</span>
            <nuxt-link to="https://github.com/ingallz" class="mx-1 text-primary">@ingallz</nuxt-link>
            <span>with</span>
            <Icon name="material-symbols:favorite-rounded" class="h-4 w-4 text-primary ml-1" />
          </div>
        </div>
      </div>
      
      <!-- Scroll Indicator -->
      <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2 animate-bounce">
        <Icon name="mdi:chevron-down" class="h-6 w-6 text-primary" />
      </div>
    </section>
    
    <!-- Features Section -->
    <section id="features" class="py-20 bg-gray-900/50">
      <div class="container mx-auto px-4">
        <div class="text-center mb-16">
          <h2 class="text-3xl font-bold text-white mb-4">Key Features</h2>
          <p class="text-gray-400 max-w-2xl mx-auto">Explore a wide range of Vue.js and Nuxt concepts through interactive examples and comprehensive guides.</p>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 max-w-5xl mx-auto">
          <div class="bg-gray-800/50 rounded-xl p-6 border border-gray-700 backdrop-blur-sm hover:border-primary/20 transition-all duration-300">
            <div class="rounded-full bg-primary/10 p-3 inline-block mb-4">
              <Icon name="mdi:school" class="h-6 w-6 text-primary" />
            </div>
            <h3 class="text-xl font-semibold text-white mb-2">Educational Content</h3>
            <p class="text-gray-400">Detailed examples and explanations of Vue.js concepts and patterns.</p>
          </div>
          
          <div class="bg-gray-800/50 rounded-xl p-6 border border-gray-700 backdrop-blur-sm hover:border-primary/20 transition-all duration-300">
            <div class="rounded-full bg-cyan-500/10 p-3 inline-block mb-4">
              <Icon name="mdi:code-tags" class="h-6 w-6 text-cyan-400" />
            </div>
            <h3 class="text-xl font-semibold text-white mb-2">Best Practices</h3>
            <p class="text-gray-400">Learn industry-standard approaches to building scalable Vue applications.</p>
          </div>
          
          <div class="bg-gray-800/50 rounded-xl p-6 border border-gray-700 backdrop-blur-sm hover:border-primary/20 transition-all duration-300">
            <div class="rounded-full bg-green-500/10 p-3 inline-block mb-4">
              <Icon name="mdi:puzzle" class="h-6 w-6 text-green-400" />
            </div>
            <h3 class="text-xl font-semibold text-white mb-2">Interactive Examples</h3>
            <p class="text-gray-400">Hands-on demos to help you understand concepts through practical application.</p>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Demo Pages Section -->
    <section class="py-20 bg-gradient-to-b from-gray-900 to-background">
      <div class="container mx-auto px-4">
        <div class="text-center mb-12">
          <h2 class="text-3xl font-bold text-white mb-4">Demo Pages</h2>
          <p class="text-gray-400 max-w-2xl mx-auto">Explore our comprehensive collection of educational modules covering key Vue.js and Nuxt concepts.</p>
        </div>
        
        <div class="max-w-4xl mx-auto grid grid-cols-1 md:grid-cols-2 gap-6">
          <nuxt-link
            v-for="page in pages"
            :key="page.path"
            :to="page.path"
            class="group relative overflow-hidden rounded-xl border border-gray-800 bg-gray-900/70 p-5 backdrop-blur-sm transition-all duration-300 hover:border-primary/50 hover:shadow-lg hover:shadow-primary/10"
          >
            <div class="absolute -right-8 -top-8 h-16 w-16 rounded-full bg-gradient-to-br from-primary/20 to-cyan-500/20 blur-xl transition-all duration-500 group-hover:bg-gradient-to-br group-hover:from-primary/30 group-hover:to-cyan-500/30 group-hover:blur-2xl"></div>
            
            <div class="flex items-center gap-4">
              <div class="flex h-12 w-12 items-center justify-center rounded-lg bg-gray-800 text-primary transition-all duration-300 group-hover:bg-primary/10 group-hover:text-primary">
                <Icon v-if="page.icon" :name="page.icon" class="h-6 w-6" />
              </div>
              <div class="flex-1">
                <h3 class="font-medium text-lg text-white mb-1">{{ page.title }}</h3>
                <p class="text-sm text-gray-400">{{ page.description }}</p>
              </div>
              <div class="ml-auto">
                <Icon name="heroicons:arrow-right" class="h-5 w-5 text-gray-500 transition-all duration-300 group-hover:translate-x-1 group-hover:text-primary" />
              </div>
            </div>
          </nuxt-link>
          
          <!-- Add New Page Card (placeholder for future pages) -->
          <div class="group relative flex flex-col items-center justify-center overflow-hidden rounded-xl border border-dashed border-gray-800 bg-gray-900/30 p-8 text-center backdrop-blur-sm">
            <Icon name="mdi:plus-circle" class="h-10 w-10 text-gray-600 mb-3" />
            <p class="text-sm text-gray-500">More demo pages coming soon...</p>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Getting Started Section -->
    <section class="py-20 bg-gray-900/50">
      <div class="container mx-auto px-4">
        <div class="max-w-4xl mx-auto bg-gray-800/30 rounded-2xl border border-gray-700 overflow-hidden backdrop-blur-sm">
          <div class="p-8 md:p-10">
            <div class="flex items-center gap-4 mb-6">
              <div class="rounded-full bg-primary/20 p-3">
                <Icon name="mdi:rocket-launch" class="h-6 w-6 text-primary" />
              </div>
              <h2 class="text-2xl font-bold text-white">Ready to Get Started?</h2>
            </div>
            
            <p class="text-gray-400 mb-8">
              Clone this repository and start exploring the different examples to learn about Vue.js and Nuxt.js development patterns and best practices.
            </p>
            
            <div class="bg-black/30 rounded-lg p-4 mb-6">
              <pre class="text-sm text-gray-300 overflow-x-auto">git clone https://github.com/ingallz/nuxt-structure.git
cd nuxt-structure
npm install
npm run dev</pre>
            </div>
            
            <div class="flex flex-wrap gap-4">
              <nuxt-link
                to="https://github.com/ingallz/nuxt-structure#readme"
                class="rounded-full bg-primary/10 border border-primary/20 px-6 py-2 text-sm font-medium text-primary transition duration-300 hover:bg-primary/20"
              >
                View Documentation
              </nuxt-link>
              <nuxt-link
                to="https://github.com/ingallz/nuxt-structure/issues"
                class="rounded-full bg-gray-800 border border-gray-700 px-6 py-2 text-sm font-medium text-white transition duration-300 hover:bg-gray-700"
              >
                Report Issues
              </nuxt-link>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Footer -->
    <footer class="py-8 border-t border-gray-800">
      <div class="container mx-auto px-4">
        <div class="flex flex-col md:flex-row items-center justify-between gap-4">
          <div class="flex items-center">
            <span class="text-primary font-semibold">Nuxt Structure</span>
            <span class="mx-2 text-gray-600">•</span>
            <span class="text-sm text-gray-500">Educational Project</span>
          </div>
          
          <div class="flex items-center gap-6">
            <a href="https://github.com/ingallz" class="text-gray-500 hover:text-primary transition-colors">
              <Icon name="mdi:github" class="h-5 w-5" />
            </a>
            <a href="https://nuxt.com" class="text-gray-500 hover:text-primary transition-colors">
              <Icon name="simple-icons:nuxtdotjs" class="h-5 w-5" />
            </a>
            <a href="https://vuejs.org" class="text-gray-500 hover:text-primary transition-colors">
              <Icon name="mdi:vuejs" class="h-5 w-5" />
            </a>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup lang="ts">
// Enhanced list of pages for navigation
const pages = [
  {
    title: 'Lifecycle Hooks',
    description: 'Learn the differences between lifecycle hooks',
    path: '/lifecycle-hooks',
    icon: 'mdi:clock-time-eight-outline',
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
  {
    title: 'API Integration',
    description: 'Axios and Fetch API for HTTP requests',
    path: '/api-integration',
    icon: 'mdi:api',
  },
  {
    title: 'Performance Optimization',
    description: 'Lazy loading and code splitting techniques',
    path: '/performance-optimization',
    icon: 'mdi:speedometer',
  },
  {
    title: 'Authentication',
    description: 'Implementation with @nuxtjs/auth-next',
    path: '/authentication',
    icon: 'mdi:account-lock',
  },
  {
    title: 'Utility Libraries',
    description: 'Lodash, Moment.js and other helpful tools',
    path: '/utility-libraries',
    icon: 'mdi:tools',
  },
];
</script>

<style>
/* Animation for scroll indicator */
@keyframes bounce {
  0%, 100% {
    transform: translateY(0) translateX(-50%);
  }
  50% {
    transform: translateY(-10px) translateX(-50%);
  }
}

.animate-bounce {
  animation: bounce 2s infinite;
}

/* Smooth scrolling */
html {
  scroll-behavior: smooth;
}
</style>
