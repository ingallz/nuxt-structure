<template>
  <div class="min-h-screen bg-background p-8">
    <h1 class="mb-4 text-center text-4xl font-bold text-primary">Performance Optimization</h1>
    <p class="mb-10 text-center text-gray-400">Techniques for improving Nuxt.js application performance</p>
    
    <div class="mt-4 flex flex-wrap justify-center gap-4">
      <button 
        v-for="(section, index) in sections" 
        :key="index"
        @click="activeSection = section.id"
        class="rounded-full px-4 py-2 text-sm font-medium transition-colors"
        :class="activeSection === section.id 
          ? 'bg-primary text-background' 
          : 'bg-gray-800 text-gray-300 hover:bg-gray-700'"
      >
        {{ section.name }}
      </button>
    </div>
    
    <!-- Lazy Loading Section -->
    <section v-if="activeSection === 'lazy-loading'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Lazy Loading</h2>
      
      <div class="mx-auto max-w-3xl rounded-lg border border-purple-500/30 bg-purple-500/5 p-6">
        <div class="mb-6 flex items-center justify-between">
          <h3 class="text-xl font-semibold text-purple-400">Component Lazy Loading</h3>
          <span class="rounded-full bg-purple-500/20 px-3 py-1 text-xs text-purple-300">
            defineAsyncComponent
          </span>
        </div>
        
        <!-- Lazy Loading Demo -->
        <div class="mb-6 grid gap-6 md:grid-cols-2">
          <div class="rounded-lg border border-gray-700 bg-gray-800 p-4">
            <h4 class="mb-4 text-sm font-medium text-white">Lazy Load Components</h4>
            <p class="mb-2 text-xs text-gray-400">Click buttons to lazy load components:</p>
            
            <div class="flex flex-col gap-3">
              <button 
                @click="loadHeavyComponent1"
                class="w-full rounded bg-purple-500/20 px-3 py-2 text-sm text-purple-300 hover:bg-purple-500/30"
              >
                Load Chart Component
              </button>
              
              <button 
                @click="loadHeavyComponent2"
                class="w-full rounded bg-purple-500/20 px-3 py-2 text-sm text-purple-300 hover:bg-purple-500/30"
              >
                Load DataTable Component
              </button>
              
              <button 
                @click="unloadComponents"
                class="mt-2 w-full rounded border border-gray-600 px-3 py-2 text-xs text-gray-400 hover:bg-gray-700"
              >
                Unload Components
              </button>
            </div>
            
            <div class="mt-4">
              <div class="flex items-center gap-2">
                <div class="h-2 w-2 rounded-full" :class="isComponent1Loaded ? 'bg-green-500' : 'bg-gray-600'"></div>
                <span class="text-xs text-gray-400">Chart Component</span>
              </div>
              <div class="mt-1 flex items-center gap-2">
                <div class="h-2 w-2 rounded-full" :class="isComponent2Loaded ? 'bg-green-500' : 'bg-gray-600'"></div>
                <span class="text-xs text-gray-400">DataTable Component</span>
              </div>
            </div>
          </div>
          
          <div class="flex flex-col rounded-lg border border-gray-700 bg-gray-800 p-4">
            <h4 class="mb-4 text-sm font-medium text-white">Lazy Loaded Content</h4>
            
            <div class="flex-1 rounded bg-gray-900 p-4">
              <div v-if="isComponent1Loaded || isComponent2Loaded" class="flex h-full flex-col items-center justify-center">
                <div v-if="isComponent1Loaded" class="w-full">
                  <div class="flex items-center justify-between">
                    <h5 class="text-xs font-medium text-purple-300">Chart Component</h5>
                    <span class="rounded bg-purple-500/20 px-2 py-0.5 text-xs text-purple-300">Loaded</span>
                  </div>
                  
                  <!-- Simulated Chart Component -->
                  <div class="mt-2 h-32 w-full overflow-hidden rounded bg-gray-800 p-2">
                    <div class="flex h-full items-end justify-around">
                      <div v-for="value in chartData" :key="value" 
                        class="w-4 bg-gradient-to-t from-purple-500 to-purple-300"
                        :style="{ height: `${value}%` }"
                      ></div>
                    </div>
                  </div>
                </div>
                
                <div v-if="isComponent2Loaded" class="mt-4 w-full">
                  <div class="flex items-center justify-between">
                    <h5 class="text-xs font-medium text-purple-300">DataTable Component</h5>
                    <span class="rounded bg-purple-500/20 px-2 py-0.5 text-xs text-purple-300">Loaded</span>
                  </div>
                  
                  <!-- Simulated DataTable Component -->
                  <div class="mt-2 w-full overflow-hidden rounded bg-gray-800">
                    <table class="w-full text-left text-xs text-gray-300">
                      <thead class="bg-gray-700 text-xs uppercase text-gray-400">
                        <tr>
                          <th scope="col" class="p-2">ID</th>
                          <th scope="col" class="p-2">Name</th>
                          <th scope="col" class="p-2">Value</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="(item, index) in tableData" :key="index" class="border-t border-gray-700">
                          <td class="p-2">{{ item.id }}</td>
                          <td class="p-2">{{ item.name }}</td>
                          <td class="p-2">{{ item.value }}</td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                </div>
              </div>
              
              <div v-else class="flex h-full items-center justify-center">
                <p class="text-sm text-gray-500">No components loaded yet</p>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Vue 3 Lazy Loading Code -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Vue 3 Component Lazy Loading</h4>
          <pre class="overflow-x-auto rounded bg-gray-800 p-4 text-xs text-gray-300"><code>import { defineAsyncComponent } from 'vue'

// Basic usage
const LazyComponent = defineAsyncComponent(() => 
  import('./components/HeavyComponent.vue')
)

// With loading and error states
const LazyComponentWithOptions = defineAsyncComponent({
  // The factory function
  loader: () => import('./components/HeavyComponent.vue'),
  
  // Component to use while loading
  loadingComponent: LoadingSpinner,
  
  // Delay before showing the loading component (default: 200ms)
  delay: 200,
  
  // Component to use if loading fails
  errorComponent: ErrorComponent,
  
  // If error component is provided, the error will be passed as a prop
  onError(error, retry, fail, attempts) {
    if (attempts &lt;= 3) {
      // Retry on error
      retry()
    } else {
      // Handle failure
      fail()
    }
  },
})</code></pre>
        </div>
        
        <!-- Nuxt Lazy Loading -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Nuxt.js Lazy Loading Options</h4>
          
          <div class="mb-4">
            <h5 class="mb-2 text-xs font-medium text-purple-300">1. Component lazy loading with defineAsyncComponent:</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">// components/MyLazyComponent.client.js
export default defineAsyncComponent(() => 
  import('./ActualComponent.vue')
)</pre>
          </div>
          
          <div class="mb-4">
            <h5 class="mb-2 text-xs font-medium text-purple-300">2. Nuxt automatic lazy loading with .lazy.vue suffix:</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">// components/
HeavyChart.lazy.vue      // Will be lazy loaded automatically
HeavyTable.vue           // Will be loaded normally</pre>
          </div>
          
          <div class="mb-4">
            <h5 class="mb-2 text-xs font-medium text-purple-300">3. Lazy loading pages in Nuxt 3:</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">// nuxt.config.ts
export default defineNuxtConfig({
  routeRules: {
    '/admin/**': { lazy: true }  // Lazy load all admin pages
  }
})</pre>
          </div>
          
          <div>
            <h5 class="mb-2 text-xs font-medium text-purple-300">4. Dynamic imports in script setup:</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">&lt;script setup&gt;
const LazyComponent = defineAsyncComponent(() => 
  import('../components/HeavyComponent.vue')
)
&lt;/script&gt;</pre>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Code Splitting Section -->
    <section v-if="activeSection === 'code-splitting'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Code Splitting</h2>
      
      <div class="mx-auto max-w-3xl rounded-lg border border-teal-500/30 bg-teal-500/5 p-6">
        <div class="mb-6 flex items-center justify-between">
          <h3 class="text-xl font-semibold text-teal-400">Automatic & Manual Code Splitting</h3>
          <span class="rounded-full bg-teal-500/20 px-3 py-1 text-xs text-teal-300">
            Webpack / Vite
          </span>
        </div>
        
        <!-- Code Splitting Visualization -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-800 p-4">
          <h4 class="mb-4 text-sm font-medium text-white">Bundle Visualization</h4>
          
          <div class="relative h-80 rounded bg-gray-900 p-4">
            <!-- Main bundle -->
            <div class="absolute left-1/2 top-1/4 h-16 w-36 -translate-x-1/2 transform rounded bg-teal-500/30 p-2 text-center text-xs font-medium text-teal-300">
              main.js
              <div class="mt-1 text-xs text-teal-200/70">Core Application</div>
            </div>
            
            <!-- Bundle chunks -->
            <div class="absolute left-1/4 top-1/2 h-14 w-32 -translate-x-1/2 transform rounded bg-green-500/30 p-2 text-center text-xs font-medium text-green-300">
              vendors.js
              <div class="mt-1 text-xs text-green-200/70">Third-party libraries</div>
            </div>
            
            <div class="absolute left-2/3 top-2/3 h-14 w-32 -translate-x-1/2 transform rounded bg-purple-500/30 p-2 text-center text-xs font-medium text-purple-300">
              pages/about.js
              <div class="mt-1 text-xs text-purple-200/70">About page chunk</div>
            </div>
            
            <div class="absolute left-1/3 top-2/3 h-14 w-32 -translate-x-1/2 transform rounded bg-blue-500/30 p-2 text-center text-xs font-medium text-blue-300">
              pages/home.js
              <div class="mt-1 text-xs text-blue-200/70">Home page chunk</div>
            </div>
            
            <!-- Connection lines -->
            <svg class="absolute inset-0 h-full w-full" xmlns="http://www.w3.org/2000/svg">
              <line x1="50%" y1="32%" x2="25%" y2="50%" stroke="#0d9488" stroke-width="1" stroke-dasharray="4" />
              <line x1="50%" y1="32%" x2="67%" y2="66%" stroke="#8b5cf6" stroke-width="1" stroke-dasharray="4" />
              <line x1="50%" y1="32%" x2="33%" y2="66%" stroke="#3b82f6" stroke-width="1" stroke-dasharray="4" />
              <line x1="25%" y1="50%" x2="33%" y2="66%" stroke="#10b981" stroke-width="1" stroke-dasharray="4" />
            </svg>
            
            <div class="absolute bottom-4 left-0 right-0 text-center text-xs text-gray-400">
              Webpack/Vite automatically splits your code into optimized chunks
            </div>
          </div>
        </div>
        
        <!-- Code Splitting Examples -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Dynamic Import Examples</h4>
          <pre class="overflow-x-auto rounded bg-gray-800 p-4 text-xs text-gray-300"><code>// Dynamic import syntax - creates a separate chunk
import('./modules/heavyModule.js').then(module => {
  // Use the module
  module.doSomething()
})

// With async/await
async function loadFeature() {
  const module = await import('./modules/feature.js')
  module.initialize()
}

// Dynamic import with named exports
const { format, parse } = await import('./modules/dateUtils.js')

// Dynamic import with comments for webpack
import(
  /* webpackChunkName: "admin" */ 
  './modules/admin.js'
)</code></pre>
        </div>
        
        <!-- Nuxt Code Splitting Configuration -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Nuxt.js Code Splitting Configuration</h4>
          
          <div class="mb-4">
            <h5 class="mb-2 text-xs font-medium text-teal-300">1. Automatic code splitting by pages:</h5>
            <p class="mb-2 text-xs text-gray-400">Nuxt automatically creates separate chunks for each page by default.</p>
          </div>
          
          <div class="mb-4">
            <h5 class="mb-2 text-xs font-medium text-teal-300">2. Custom webpack configuration (Nuxt 2):</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">// nuxt.config.js
export default {
  build: {
    splitChunks: {
      layouts: true,
      pages: true,
      commons: true
    }
  }
}</pre>
          </div>
          
          <div class="mb-4">
            <h5 class="mb-2 text-xs font-medium text-teal-300">3. Vite configuration (Nuxt 3):</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">// nuxt.config.ts
export default defineNuxtConfig({
  vite: {
    build: {
      rollupOptions: {
        output: {
          manualChunks: {
            'group-user': [
              './composables/useAuth.ts',
              './composables/useUser.ts'
            ],
            'group-product': [
              './composables/useProduct.ts',
              './composables/useCart.ts'
            ]
          }
        }
      }
    }
  }
})</pre>
          </div>
          
          <div>
            <h5 class="mb-2 text-xs font-medium text-teal-300">4. Prefetching optimization:</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">// nuxt.config.ts
export default defineNuxtConfig({
  app: {
    head: {
      htmlAttrs: {
        lang: 'en'
      }
    }
  },
  router: {
    prefetchLinks: true  // Default is true in Nuxt 2
  }
})</pre>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Benefits Section -->
    <section v-if="activeSection === 'benefits'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Performance Benefits</h2>
      
      <div class="mx-auto max-w-3xl overflow-x-auto rounded-lg border border-gray-700">
        <table class="w-full text-left text-sm text-gray-300">
          <thead class="bg-gray-800 text-xs uppercase text-gray-400">
            <tr>
              <th scope="col" class="p-4">Technique</th>
              <th scope="col" class="p-4">Benefits</th>
              <th scope="col" class="p-4">Trade-offs</th>
            </tr>
          </thead>
          <tbody>
            <tr class="border-b border-gray-700">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-purple-300">Lazy Loading</th>
              <td class="p-4">
                <ul class="list-inside list-disc text-xs">
                  <li>Reduces initial load time</li>
                  <li>Only loads what's needed</li>
                  <li>Improves time-to-interactive</li>
                </ul>
              </td>
              <td class="p-4">
                <ul class="list-inside list-disc text-xs">
                  <li>Can cause loading delays when component is needed</li>
                  <li>More HTTP requests</li>
                </ul>
              </td>
            </tr>
            <tr class="border-b border-gray-700 bg-gray-800/30">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-teal-300">Code Splitting</th>
              <td class="p-4">
                <ul class="list-inside list-disc text-xs">
                  <li>Smaller initial bundle size</li>
                  <li>Faster page loads</li>
                  <li>Better caching</li>
                </ul>
              </td>
              <td class="p-4">
                <ul class="list-inside list-disc text-xs">
                  <li>More HTTP requests</li>
                  <li>May require additional configuration</li>
                </ul>
              </td>
            </tr>
            <tr class="border-b border-gray-700">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-yellow-300">Prefetching</th>
              <td class="p-4">
                <ul class="list-inside list-disc text-xs">
                  <li>Preloads resources before needed</li>
                  <li>Makes navigation feel instant</li>
                </ul>
              </td>
              <td class="p-4">
                <ul class="list-inside list-disc text-xs">
                  <li>Can waste bandwidth if unused</li>
                  <li>May not be suitable for limited data plans</li>
                </ul>
              </td>
            </tr>
            <tr class="border-b border-gray-700 bg-gray-800/30">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-blue-300">Tree Shaking</th>
              <td class="p-4">
                <ul class="list-inside list-disc text-xs">
                  <li>Eliminates unused code</li>
                  <li>Reduces bundle size</li>
                </ul>
              </td>
              <td class="p-4">
                <ul class="list-inside list-disc text-xs">
                  <li>Requires ES modules syntax</li>
                  <li>May be complex to configure properly</li>
                </ul>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
      
      <!-- Performance Metrics Visualization -->
      <div class="mx-auto mt-6 max-w-3xl rounded-lg border border-gray-700 bg-gray-900 p-4">
        <h4 class="mb-4 text-sm font-medium text-white">Performance Improvements</h4>
        
        <div class="space-y-4">
          <div>
            <div class="mb-1 flex items-center justify-between">
              <span class="text-xs text-gray-400">Initial Load Time</span>
              <span class="text-xs font-medium text-gray-400">-65%</span>
            </div>
            <div class="h-2 rounded-full bg-gray-700">
              <div class="h-2 w-3/4 rounded-full bg-gradient-to-r from-green-500 to-green-300"></div>
            </div>
          </div>
          
          <div>
            <div class="mb-1 flex items-center justify-between">
              <span class="text-xs text-gray-400">Bundle Size</span>
              <span class="text-xs font-medium text-gray-400">-70%</span>
            </div>
            <div class="h-2 rounded-full bg-gray-700">
              <div class="h-2 w-4/5 rounded-full bg-gradient-to-r from-blue-500 to-blue-300"></div>
            </div>
          </div>
          
          <div>
            <div class="mb-1 flex items-center justify-between">
              <span class="text-xs text-gray-400">Time to Interactive</span>
              <span class="text-xs font-medium text-gray-400">-50%</span>
            </div>
            <div class="h-2 rounded-full bg-gray-700">
              <div class="h-2 w-1/2 rounded-full bg-gradient-to-r from-purple-500 to-purple-300"></div>
            </div>
          </div>
          
          <div>
            <div class="mb-1 flex items-center justify-between">
              <span class="text-xs text-gray-400">Lighthouse Score</span>
              <span class="text-xs font-medium text-gray-400">+40%</span>
            </div>
            <div class="h-2 rounded-full bg-gray-700">
              <div class="h-2 w-2/5 rounded-full bg-gradient-to-r from-yellow-500 to-yellow-300"></div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue';

// Section navigation
const sections = [
  { id: 'lazy-loading', name: 'Lazy Loading' },
  { id: 'code-splitting', name: 'Code Splitting' },
  { id: 'benefits', name: 'Performance Benefits' }
];
const activeSection = ref('lazy-loading');

// Lazy loading demo
const isComponent1Loaded = ref(false);
const isComponent2Loaded = ref(false);

// Mock chart data
const chartData = reactive([25, 40, 65, 30, 85, 55, 70, 60]);

// Mock table data
const tableData = reactive([
  { id: 1, name: 'Item A', value: 42 },
  { id: 2, name: 'Item B', value: 78 },
  { id: 3, name: 'Item C', value: 15 },
  { id: 4, name: 'Item D', value: 63 }
]);

// Simulate component loading
function loadHeavyComponent1() {
  setTimeout(() => {
    isComponent1Loaded.value = true;
  }, 800);
}

function loadHeavyComponent2() {
  setTimeout(() => {
    isComponent2Loaded.value = true;
  }, 1000);
}

function unloadComponents() {
  isComponent1Loaded.value = false;
  isComponent2Loaded.value = false;
}
</script> 