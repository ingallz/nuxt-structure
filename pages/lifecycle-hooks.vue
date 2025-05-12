<template>
  <div class="min-h-screen bg-background p-8">
    <h1 class="mb-4 text-center text-4xl font-bold text-primary">Nuxt Lifecycle Hooks</h1>
    <p class="mb-10 text-center text-gray-400">Understanding the differences between <span class="text-primary">Created</span>, <span class="text-yellow-400">BeforeMount</span>, and <span class="text-cyan-400">Mounted</span> hooks</p>
    
    <!-- Timeline visualization -->
    <div class="mb-12 hidden md:block">
      <div class="relative mx-auto h-24 max-w-3xl">
        <!-- Timeline line -->
        <div class="absolute left-0 top-1/2 h-1 w-full -translate-y-1/2 bg-gray-700"></div>
        
        <!-- Created step -->
        <div class="absolute left-0 top-0 flex w-1/3 flex-col items-center">
          <div class="flex h-12 w-12 items-center justify-center rounded-full border-4 border-primary bg-gray-900">
            <Icon name="mdi:code-braces" class="h-5 w-5 text-primary" />
          </div>
          <div class="mt-2 text-center">
            <p class="font-semibold text-primary">Created</p>
            <p class="text-xs text-gray-400">Instance created</p>
          </div>
        </div>
        
        <!-- BeforeMount step -->
        <div class="absolute left-1/3 top-0 flex w-1/3 -translate-x-1/2 flex-col items-center">
          <div class="flex h-12 w-12 items-center justify-center rounded-full border-4 border-yellow-400 bg-gray-900">
            <Icon name="mdi:view-dashboard-outline" class="h-5 w-5 text-yellow-400" />
          </div>
          <div class="mt-2 text-center">
            <p class="font-semibold text-yellow-400">BeforeMount</p>
            <p class="text-xs text-gray-400">Template compiled</p>
          </div>
        </div>
        
        <!-- Mounted step -->
        <div class="absolute right-0 top-0 flex w-1/3 flex-col items-center">
          <div class="flex h-12 w-12 items-center justify-center rounded-full border-4 border-cyan-400 bg-gray-900">
            <Icon name="mdi:monitor-dashboard" class="h-5 w-5 text-cyan-400" />
          </div>
          <div class="mt-2 text-center">
            <p class="font-semibold text-cyan-400">Mounted</p>
            <p class="text-xs text-gray-400">DOM accessible</p>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Comparison table -->
    <div class="mb-10 overflow-x-auto rounded-lg border border-gray-700">
      <table class="w-full text-left text-sm text-gray-300">
        <thead class="bg-gray-800 text-xs uppercase text-gray-400">
          <tr>
            <th scope="col" class="p-4">Feature</th>
            <th scope="col" class="p-4 text-primary">Created</th>
            <th scope="col" class="p-4 text-yellow-400">BeforeMount</th>
            <th scope="col" class="p-4 text-cyan-400">Mounted</th>
          </tr>
        </thead>
        <tbody>
          <tr class="border-b border-gray-700">
            <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">Timing</th>
            <td class="p-4">After instance creation</td>
            <td class="p-4">Right before DOM mounting</td>
            <td class="p-4">After DOM is mounted</td>
          </tr>
          <tr class="border-b border-gray-700 bg-gray-800/30">
            <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">DOM Access</th>
            <td class="p-4">❌ Not available</td>
            <td class="p-4">❌ Not available</td>
            <td class="p-4">✅ Available</td>
          </tr>
          <tr class="border-b border-gray-700">
            <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">Data Manipulation</th>
            <td class="p-4">✅ Available</td>
            <td class="p-4">✅ Available</td>
            <td class="p-4">✅ Available</td>
          </tr>
          <tr class="border-b border-gray-700 bg-gray-800/30">
            <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">Use Cases</th>
            <td class="p-4">Initialize data, API calls</td>
            <td class="p-4">Last-minute data prep</td>
            <td class="p-4">DOM manipulation, third-party libraries</td>
          </tr>
          <tr class="bg-gray-800/30">
            <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">Composition API</th>
            <td class="p-4">Top-level code</td>
            <td class="p-4"><code class="bg-gray-800 px-1 py-0.5 rounded">onBeforeMount()</code></td>
            <td class="p-4"><code class="bg-gray-800 px-1 py-0.5 rounded">onMounted()</code></td>
          </tr>
        </tbody>
      </table>
    </div>
    
    <!-- Live Demo Cards -->
    <h2 class="mb-6 text-center text-2xl font-bold text-white">Live Demo</h2>
    <div class="grid gap-8 md:grid-cols-3">
      <!-- Created Hook -->
      <div class="relative rounded-lg border border-primary bg-gray-900 p-6">
        <div class="absolute -right-2 -top-2 flex h-8 w-8 items-center justify-center rounded-full bg-primary text-xs font-bold text-background">1</div>
        <h2 class="mb-4 flex items-center gap-2 text-2xl font-semibold text-primary">
          <Icon name="mdi:code-braces" class="h-6 w-6" />
          Created
        </h2>
        <div class="mb-4 rounded border border-primary/30 bg-primary/5 p-3">
          <p class="text-sm text-gray-300">
            The <code class="bg-gray-800 px-1 py-0.5 rounded">created()</code> hook runs after the instance has been created, but before the DOM has been mounted.
          </p>
        </div>
        <div class="space-y-3">
          <div class="rounded bg-gray-800 p-3">
            <h3 class="mb-2 flex items-center gap-1.5 font-medium text-primary">
              <Icon name="mdi:console" class="h-4 w-4" />
              Log Output:
            </h3>
            <ul class="space-y-1.5 text-sm">
              <li v-for="(log, index) in createdLogs" :key="index" class="text-white">
                {{ log }}
              </li>
            </ul>
          </div>
          <div class="grid grid-cols-2 gap-3">
            <div class="rounded bg-gray-800 p-3">
              <h3 class="mb-1 text-xs font-medium text-gray-400">Data Access:</h3>
              <p class="text-sm font-medium text-green-400">Available ✓</p>
              <p class="mt-1 text-xs text-gray-400">Value: <span class="text-white">{{ createdData }}</span></p>
            </div>
            <div class="rounded bg-gray-800 p-3">
              <h3 class="mb-1 text-xs font-medium text-gray-400">DOM Access:</h3>
              <p class="text-sm font-medium text-red-400">Not Available ✗</p>
              <p class="mt-1 text-xs text-gray-400">Status: <span class="text-white">{{ createdDomStatus }}</span></p>
            </div>
          </div>
        </div>
      </div>

      <!-- BeforeMount Hook -->
      <div class="relative rounded-lg border border-yellow-400 bg-gray-900 p-6">
        <div class="absolute -right-2 -top-2 flex h-8 w-8 items-center justify-center rounded-full bg-yellow-400 text-xs font-bold text-background">2</div>
        <h2 class="mb-4 flex items-center gap-2 text-2xl font-semibold text-yellow-400">
          <Icon name="mdi:view-dashboard-outline" class="h-6 w-6" />
          BeforeMount
        </h2>
        <div class="mb-4 rounded border border-yellow-400/30 bg-yellow-400/5 p-3">
          <p class="text-sm text-gray-300">
            The <code class="bg-gray-800 px-1 py-0.5 rounded">beforeMount()</code> hook runs right before the DOM is about to be mounted.
          </p>
        </div>
        <div class="space-y-3">
          <div class="rounded bg-gray-800 p-3">
            <h3 class="mb-2 flex items-center gap-1.5 font-medium text-yellow-400">
              <Icon name="mdi:console" class="h-4 w-4" />
              Log Output:
            </h3>
            <ul class="space-y-1.5 text-sm">
              <li v-for="(log, index) in beforeMountLogs" :key="index" class="text-white">
                {{ log }}
              </li>
            </ul>
          </div>
          <div class="grid grid-cols-2 gap-3">
            <div class="rounded bg-gray-800 p-3">
              <h3 class="mb-1 text-xs font-medium text-gray-400">Data Access:</h3>
              <p class="text-sm font-medium text-green-400">Available ✓</p>
              <p class="mt-1 text-xs text-gray-400">Value: <span class="text-white">{{ beforeMountData }}</span></p>
            </div>
            <div class="rounded bg-gray-800 p-3">
              <h3 class="mb-1 text-xs font-medium text-gray-400">DOM Access:</h3>
              <p class="text-sm font-medium text-red-400">Not Available ✗</p>
              <p class="mt-1 text-xs text-gray-400">Status: <span class="text-white">{{ beforeMountDomStatus }}</span></p>
            </div>
          </div>
        </div>
      </div>

      <!-- Mounted Hook -->
      <div class="relative rounded-lg border border-cyan-400 bg-gray-900 p-6">
        <div class="absolute -right-2 -top-2 flex h-8 w-8 items-center justify-center rounded-full bg-cyan-400 text-xs font-bold text-background">3</div>
        <h2 class="mb-4 flex items-center gap-2 text-2xl font-semibold text-cyan-400">
          <Icon name="mdi:monitor-dashboard" class="h-6 w-6" />
          Mounted
        </h2>
        <div class="mb-4 rounded border border-cyan-400/30 bg-cyan-400/5 p-3">
          <p class="text-sm text-gray-300">
            The <code class="bg-gray-800 px-1 py-0.5 rounded">mounted()</code> hook runs after the DOM has been mounted and is accessible.
          </p>
        </div>
        <div class="space-y-3">
          <div class="rounded bg-gray-800 p-3">
            <h3 class="mb-2 flex items-center gap-1.5 font-medium text-cyan-400">
              <Icon name="mdi:console" class="h-4 w-4" />
              Log Output:
            </h3>
            <ul class="space-y-1.5 text-sm">
              <li v-for="(log, index) in mountedLogs" :key="index" class="text-white">
                {{ log }}
              </li>
            </ul>
          </div>
          <div class="grid grid-cols-2 gap-3">
            <div class="rounded bg-gray-800 p-3">
              <h3 class="mb-1 text-xs font-medium text-gray-400">Data Access:</h3>
              <p class="text-sm font-medium text-green-400">Available ✓</p>
              <p class="mt-1 text-xs text-gray-400">Value: <span class="text-white">{{ mountedData }}</span></p>
            </div>
            <div class="rounded bg-gray-800 p-3">
              <h3 class="mb-1 text-xs font-medium text-gray-400">DOM Access:</h3>
              <p class="text-sm font-medium text-green-400">Available ✓</p>
              <p class="mt-1 text-xs text-gray-400">Status: <span class="text-white">{{ mountedDomStatus }}</span></p>
            </div>
          </div>
          <div class="rounded bg-gray-800 p-3">
            <h3 class="mb-1 text-xs font-medium text-gray-400">DOM Measurement:</h3>
            <div class="flex items-center justify-between">
              <p class="text-sm text-white">Element Width: <span class="font-medium text-cyan-400">{{ elementWidth }}px</span></p>
              <Icon name="mdi:ruler" class="h-5 w-5 text-cyan-400" />
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Example DOM element that will be measured -->
    <div ref="exampleElement" class="mt-8 rounded-lg border-2 border-dashed border-cyan-400 bg-gray-800 p-6 text-center">
      <div class="flex items-center justify-center gap-2">
        <Icon name="mdi:ruler-square" class="h-6 w-6 text-cyan-400" />
        <p class="text-lg text-white">This element's width is measured in the <span class="font-medium text-cyan-400">mounted</span> hook</p>
      </div>
    </div>

    <!-- Execution Order -->
    <div class="mt-12 rounded-lg border border-gray-700 bg-gray-900 p-6">
      <h2 class="mb-4 flex items-center gap-2 text-2xl font-semibold text-white">
        <Icon name="mdi:order-numeric-ascending" class="h-6 w-6 text-primary" />
        Execution Order
      </h2>
      <div class="relative pl-8">
        <div class="absolute left-3 top-0 h-full w-0.5 bg-gradient-to-b from-primary via-yellow-400 to-cyan-400"></div>
        <ol class="space-y-4">
          <li v-for="(step, index) in executionOrder" :key="index" class="relative">
            <div class="absolute -left-8 top-0 flex h-6 w-6 items-center justify-center rounded-full" 
                 :class="{
                   'bg-primary': index === 0,
                   'bg-yellow-400': index === 1,
                   'bg-cyan-400': index === 2
                 }">
              <span class="text-xs font-bold text-background">{{ index + 1 }}</span>
            </div>
            <p class="text-white">{{ step }}</p>
          </li>
        </ol>
      </div>
    </div>

    <!-- Key differences summary -->
    <div class="mt-10 rounded-lg border border-gray-700 bg-gray-900 p-6">
      <h2 class="mb-4 text-2xl font-semibold text-white">Key Differences</h2>
      <div class="space-y-4">
        <div class="rounded-lg border border-primary/30 bg-primary/5 p-4">
          <h3 class="mb-2 text-lg font-medium text-primary">Created</h3>
          <ul class="list-inside list-disc space-y-1 text-sm text-gray-300">
            <li>Runs after the instance is created</li>
            <li>Data and computed properties are available</li>
            <li>DOM is <span class="font-medium text-red-400">not accessible</span></li>
            <li>Good for data initialization and API calls</li>
            <li>In Composition API: Write code at the top level of the setup function</li>
          </ul>
        </div>
        
        <div class="rounded-lg border border-yellow-400/30 bg-yellow-400/5 p-4">
          <h3 class="mb-2 text-lg font-medium text-yellow-400">BeforeMount</h3>
          <ul class="list-inside list-disc space-y-1 text-sm text-gray-300">
            <li>Runs right before the DOM is mounted</li>
            <li>Template has been compiled</li>
            <li>DOM is <span class="font-medium text-red-400">not accessible yet</span></li>
            <li>Last chance to modify data before rendering</li>
            <li>In Composition API: Use <code class="bg-gray-800 px-1 py-0.5 rounded">onBeforeMount()</code> hook</li>
          </ul>
        </div>
        
        <div class="rounded-lg border border-cyan-400/30 bg-cyan-400/5 p-4">
          <h3 class="mb-2 text-lg font-medium text-cyan-400">Mounted</h3>
          <ul class="list-inside list-disc space-y-1 text-sm text-gray-300">
            <li>Runs after the DOM has been mounted</li>
            <li>DOM elements are <span class="font-medium text-green-400">fully accessible</span></li>
            <li>Perfect for DOM manipulation and measurements</li>
            <li>Ideal for integrating third-party libraries that need DOM access</li>
            <li>In Composition API: Use <code class="bg-gray-800 px-1 py-0.5 rounded">onMounted()</code> hook</li>
          </ul>
        </div>
      </div>
    </div>

    <!-- Refresh Button -->
    <div class="mt-10 flex justify-center">
      <button 
        @click="refreshPage" 
        class="flex items-center gap-2 rounded bg-gradient-to-r from-primary to-cyan-500 px-6 py-3 font-semibold text-background transition duration-300 hover:drop-shadow-primary"
      >
        <Icon name="mdi:refresh" class="h-5 w-5" />
        Refresh Page
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onBeforeMount, onMounted } from 'vue';

// Data for each lifecycle hook
const createdLogs = ref<string[]>([]);
const beforeMountLogs = ref<string[]>([]);
const mountedLogs = ref<string[]>([]);

const createdData = ref('Initialized');
const beforeMountData = ref('Initialized');
const mountedData = ref('Initialized');

const createdDomStatus = ref('Not Available');
const beforeMountDomStatus = ref('Not Available');
const mountedDomStatus = ref('Not Available');

const exampleElement = ref<HTMLElement | null>(null);
const elementWidth = ref(0);

const executionOrder = ref<string[]>([]);

// Created hook (in Composition API, this is just the top-level code)
createdLogs.value.push('Created hook executed at: ' + new Date().toLocaleTimeString());
executionOrder.value.push('Created hook executed');

// Try to access DOM in created hook (will fail)
try {
  const element = document.querySelector('#non-existent');
  createdDomStatus.value = element ? 'Available' : 'Not Available (but DOM API is accessible)';
} catch (error) {
  createdDomStatus.value = 'DOM API not accessible';
}

// Update data in created hook
createdData.value = 'Updated in created hook';

// BeforeMount hook
onBeforeMount(() => {
  beforeMountLogs.value.push('BeforeMount hook executed at: ' + new Date().toLocaleTimeString());
  executionOrder.value.push('BeforeMount hook executed');
  
  // Try to access DOM in beforeMount hook
  try {
    const element = document.querySelector('#non-existent');
    beforeMountDomStatus.value = element ? 'Available' : 'Not Available (but DOM API is accessible)';
  } catch (error) {
    beforeMountDomStatus.value = 'DOM API not accessible';
  }
  
  // Update data in beforeMount hook
  beforeMountData.value = 'Updated in beforeMount hook';
});

// Mounted hook
onMounted(() => {
  mountedLogs.value.push('Mounted hook executed at: ' + new Date().toLocaleTimeString());
  executionOrder.value.push('Mounted hook executed');
  
  // Try to access DOM in mounted hook
  try {
    const element = document.querySelector('div');
    mountedDomStatus.value = element ? 'Available' : 'Not Available';
    
    // Access the referenced DOM element
    if (exampleElement.value) {
      elementWidth.value = exampleElement.value.offsetWidth;
    }
  } catch (error) {
    mountedDomStatus.value = 'DOM API not accessible';
  }
  
  // Update data in mounted hook
  mountedData.value = 'Updated in mounted hook';
});

// Function to refresh the page
const refreshPage = () => {
  window.location.reload();
};
</script> 