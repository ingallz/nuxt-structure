<template>
  <div class="min-h-screen bg-background p-8">
    <h1 class="mb-4 text-center text-4xl font-bold text-primary">Vue.js Fundamentals</h1>
    <p class="mb-10 text-center text-gray-400">Interactive examples of core Vue.js features and patterns</p>
    
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
    
    <!-- Directives Section -->
    <section v-if="activeSection === 'directives'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Directives</h2>
      <div class="grid gap-6 md:grid-cols-2">
        <!-- v-if, v-else -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-6">
          <h3 class="mb-3 text-xl font-semibold text-cyan-400">v-if / v-else</h3>
          <p class="mb-4 text-sm text-gray-300">Conditionally render elements based on a boolean value</p>
          
          <div class="mb-4">
            <button 
              @click="showElement = !showElement" 
              class="rounded bg-primary/10 px-3 py-1 text-xs text-primary"
            >
              {{ showElement ? 'Hide' : 'Show' }}
            </button>
            
            <div class="mt-2 rounded border border-gray-700 bg-gray-800 p-4">
              <div v-if="showElement" class="text-green-400">
                This element is visible when showElement is true
              </div>
              <div v-else class="text-red-400">
                This element is visible when showElement is false
              </div>
            </div>
          </div>
        </div>
        
        <!-- v-for -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-6">
          <h3 class="mb-3 text-xl font-semibold text-cyan-400">v-for</h3>
          <p class="mb-4 text-sm text-gray-300">Render a list of items based on an array</p>
          
          <div class="mb-4">
            <div class="rounded border border-gray-700 bg-gray-800 p-4">
              <ul class="space-y-2">
                <li
                  v-for="(item, index) in items"
                  :key="index"
                  class="flex items-center justify-between rounded bg-gray-700 p-2"
                >
                  <span>{{ item.name }}</span>
                  <span class="rounded bg-primary/20 px-2 py-1 text-xs text-primary">{{ item.type }}</span>
                </li>
              </ul>
            </div>
            
            <div class="mt-2 flex justify-end">
              <button 
                @click="addItem" 
                class="rounded bg-primary/10 px-3 py-1 text-xs text-primary"
              >
                Add Item
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Computed Properties Section -->
    <section v-if="activeSection === 'computed'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Computed Properties</h2>
      <div class="mx-auto max-w-2xl rounded-lg border border-gray-700 bg-gray-900 p-6">
        <h3 class="mb-3 text-xl font-semibold text-yellow-400">Computed Properties</h3>
        <p class="mb-4 text-sm text-gray-300">Calculated properties that update when their dependencies change</p>
        
        <div class="space-y-4">
          <div>
            <label class="mb-1 block text-sm text-gray-400">First Name:</label>
            <input 
              v-model="firstName" 
              type="text" 
              class="w-full rounded border border-gray-700 bg-gray-800 p-2 text-white outline-none focus:border-primary"
            />
          </div>
          
          <div>
            <label class="mb-1 block text-sm text-gray-400">Last Name:</label>
            <input 
              v-model="lastName" 
              type="text" 
              class="w-full rounded border border-gray-700 bg-gray-800 p-2 text-white outline-none focus:border-primary"
            />
          </div>
          
          <div class="rounded bg-gray-800 p-4">
            <p class="text-sm text-gray-300">Full Name: <span class="font-medium text-yellow-400">{{ fullName }}</span></p>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Methods Section -->
    <section v-if="activeSection === 'methods'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Methods</h2>
      <div class="mx-auto max-w-2xl rounded-lg border border-gray-700 bg-gray-900 p-6">
        <h3 class="mb-3 text-xl font-semibold text-blue-400">Methods</h3>
        <p class="mb-4 text-sm text-gray-300">Functions that can be called from your templates or other functions</p>
        
        <div class="space-y-4">
          <div class="rounded bg-gray-800 p-4">
            <h4 class="mb-2 text-sm font-medium text-white">Counter Example:</h4>
            <div class="flex items-center justify-between">
              <div class="flex items-center gap-2">
                <button 
                  @click="decrementCounter" 
                  class="flex h-8 w-8 items-center justify-center rounded-full bg-gray-700 text-white hover:bg-blue-400/20"
                >
                  -
                </button>
                <span class="text-xl font-medium text-blue-400">{{ counter }}</span>
                <button 
                  @click="incrementCounter" 
                  class="flex h-8 w-8 items-center justify-center rounded-full bg-gray-700 text-white hover:bg-blue-400/20"
                >
                  +
                </button>
              </div>
              <button 
                @click="resetCounter" 
                class="rounded bg-blue-500/10 px-3 py-1 text-xs text-blue-400"
              >
                Reset
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Watchers Section -->
    <section v-if="activeSection === 'watchers'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Watchers</h2>
      <div class="mx-auto max-w-2xl rounded-lg border border-gray-700 bg-gray-900 p-6">
        <h3 class="mb-3 text-xl font-semibold text-purple-400">Watchers</h3>
        <p class="mb-4 text-sm text-gray-300">Watch for changes to reactive data and respond with side effects</p>
        
        <div class="space-y-4">
          <div>
            <label class="mb-1 block text-sm text-gray-400">Search Query:</label>
            <input 
              v-model="searchQuery" 
              type="text" 
              class="w-full rounded border border-gray-700 bg-gray-800 p-2 text-white outline-none focus:border-primary"
              placeholder="Type to search..."
            />
          </div>
          
          <div class="rounded bg-gray-800 p-4">
            <h4 class="mb-2 text-sm font-medium text-white">Search Status:</h4>
            <div class="flex items-center gap-2">
              <div v-if="isSearching" class="h-3 w-3 animate-pulse rounded-full bg-purple-400"></div>
              <p class="text-sm text-gray-300">{{ searchStatus }}</p>
            </div>
          </div>
          
          <div class="rounded-lg border border-gray-700 bg-gray-800/30 p-4">
            <h4 class="mb-2 text-sm font-medium text-white">Search History:</h4>
            <ul class="max-h-24 space-y-1 overflow-y-auto text-sm">
              <li v-for="(item, index) in searchHistory" :key="index" class="text-gray-300">
                <span class="text-xs text-gray-500">{{ index + 1 }}.</span> {{ item }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Props & Events Section -->
    <section v-if="activeSection === 'props'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Props & Events</h2>
      <div class="mx-auto max-w-2xl rounded-lg border border-gray-700 bg-gray-900 p-6">
        <h3 class="mb-3 text-xl font-semibold text-green-400">Props & Events</h3>
        <p class="mb-4 text-sm text-gray-300">Component communication with props down, events up pattern</p>
        
        <div class="rounded-lg border border-gray-800 bg-gray-800/50 p-4 mb-4">
          <h4 class="mb-2 text-sm font-medium text-white">Parent Component Controls:</h4>
          <div class="space-y-3">
            <div>
              <label class="mb-1 block text-sm text-gray-400">Message for Child:</label>
              <input 
                v-model="messageForChild" 
                type="text" 
                class="w-full rounded border border-gray-700 bg-gray-800 p-2 text-white outline-none focus:border-primary"
              />
            </div>
            <div class="flex gap-2">
              <button 
                @click="childTheme = 'light'" 
                class="rounded bg-amber-500/10 px-3 py-1 text-xs text-amber-400"
                :class="{ 'bg-amber-500/30': childTheme === 'light' }"
              >
                Light Theme
              </button>
              <button 
                @click="childTheme = 'dark'" 
                class="rounded bg-blue-500/10 px-3 py-1 text-xs text-blue-400"
                :class="{ 'bg-blue-500/30': childTheme === 'dark' }"
              >
                Dark Theme
              </button>
            </div>
          </div>
        </div>
        
        <div class="mb-4">
          <!-- Child Component Simulation -->
          <div 
            class="rounded p-4"
            :class="childTheme === 'light' ? 'bg-amber-500/10 text-amber-900' : 'bg-blue-500/10 text-blue-100'"
          >
            <div class="text-sm font-medium mb-2">Child Component (receives props)</div>
            <p>Message from parent: "{{ messageForChild }}"</p>
            <div class="mt-3">
              <button 
                @click="sendMessageToParent" 
                class="rounded px-3 py-1 text-xs"
                :class="childTheme === 'light' ? 'bg-amber-500/20 text-amber-700' : 'bg-blue-500/20 text-blue-100'"
              >
                Send Response to Parent
              </button>
            </div>
          </div>
        </div>
        
        <div v-if="messageFromChild" class="rounded-lg border border-green-500/30 bg-green-500/5 p-4">
          <h4 class="mb-2 text-sm font-medium text-white">Message from Child:</h4>
          <p class="text-green-400">{{ messageFromChild }}</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, watch } from 'vue';

// Section navigation
const sections = [
  { id: 'directives', name: 'Directives' },
  { id: 'computed', name: 'Computed Properties' },
  { id: 'watchers', name: 'Watchers' },
  { id: 'methods', name: 'Methods' },
  { id: 'props', name: 'Props & Events' }
];
const activeSection = ref('directives');

// Directives
const showElement = ref(true);
const items = ref([
  { name: 'Item 1', type: 'Default' },
  { name: 'Item 2', type: 'Default' },
  { name: 'Item 3', type: 'Default' },
]);
const addItem = () => {
  const newIndex = items.value.length + 1;
  items.value.push({ name: `Item ${newIndex}`, type: 'New' });
};

// Computed Properties
const firstName = ref('John');
const lastName = ref('Doe');

// A computed property that automatically updates when its dependencies (firstName or lastName) change
// It concatenates firstName and lastName if both exist, otherwise shows a placeholder message
// The computation is cached and only re-runs when the dependencies change
// This is more efficient than using a method which would re-run on every render
// Similar to React's useMemo hook which also memoizes computed values based on dependencies
const fullName = computed(() => {
  return firstName.value && lastName.value
    ? `${firstName.value} ${lastName.value}`
    : 'Please enter your name';
});

// Methods
const counter = ref(0);

function incrementCounter() {
  counter.value++;
}

function decrementCounter() {
  if (counter.value > 0) {
    counter.value--;
  }
}

function resetCounter() {
  counter.value = 0;
}

// Watchers
const searchQuery = ref('');
const isSearching = ref(false);
const searchHistory = ref<string[]>([]);
const searchStatus = ref('Ready');

watch(searchQuery, (newValue, oldValue) => {
  if (!newValue) {
    searchStatus.value = 'Ready';
    return;
  }
  
  searchHistory.value.push(newValue);
  isSearching.value = true;
  searchStatus.value = 'Searching...';
  
  // Simulate API call delay
  setTimeout(() => {
    isSearching.value = false;
    searchStatus.value = `Found results for "${newValue}"`;
  }, 500);
});

// Props & Events
const messageForChild = ref('Hello from parent!');
const childTheme = ref('dark');
const messageFromChild = ref('');

function sendMessageToParent() {
  messageFromChild.value = 'Hello from child! I received your message: "' + messageForChild.value + '"';
}
</script> 