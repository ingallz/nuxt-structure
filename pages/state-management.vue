<template>
  <div class="min-h-screen bg-background p-8">
    <h1 class="mb-4 text-center text-4xl font-bold text-primary">State Management</h1>
    <p class="mb-10 text-center text-gray-400">Understanding Vuex and Pinia for centralized state management</p>
    
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
    
    <!-- Vuex Section -->
    <section v-if="activeSection === 'vuex'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Vuex</h2>
      
      <div class="mx-auto max-w-3xl rounded-lg border border-indigo-500/30 bg-indigo-500/5 p-6">
        <div class="mb-6 flex items-center justify-between">
          <h3 class="text-xl font-semibold text-indigo-400">Vuex Store Simulation</h3>
          <span class="rounded-full bg-indigo-500/20 px-3 py-1 text-xs text-indigo-300">
            Store: Counter
          </span>
        </div>
        
        <!-- State Display -->
        <div class="mb-6 grid gap-6 md:grid-cols-2">
          <div class="rounded-lg border border-gray-700 bg-gray-800 p-4">
            <h4 class="mb-2 text-sm font-medium text-white">Store State</h4>
            <div class="space-y-2">
              <div class="flex items-center justify-between">
                <span class="text-xs text-gray-400">count:</span>
                <span class="text-sm font-mono text-white">{{ vuexStore.state.count }}</span>
              </div>
              <div class="flex items-center justify-between">
                <span class="text-xs text-gray-400">lastUpdated:</span>
                <span class="text-sm font-mono text-white">{{ vuexStore.state.lastUpdated }}</span>
              </div>
            </div>
          </div>
          
          <div class="rounded-lg border border-gray-700 bg-gray-800 p-4">
            <h4 class="mb-2 text-sm font-medium text-white">Getters</h4>
            <div class="space-y-2">
              <div class="flex items-center justify-between">
                <span class="text-xs text-gray-400">doubleCount:</span>
                <span class="text-sm font-mono text-white">{{ vuexStore.getters.doubleCount }}</span>
              </div>
              <div class="flex items-center justify-between">
                <span class="text-xs text-gray-400">countStatus:</span>
                <span class="rounded bg-gray-700 px-2 py-0.5 text-xs text-white">
                  {{ vuexStore.getters.countStatus }}
                </span>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Controls -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Mutations & Actions</h4>
          <div class="grid gap-4 md:grid-cols-2">
            <div>
              <p class="mb-2 text-xs text-gray-400">Mutations (Synchronous)</p>
              <div class="flex flex-wrap gap-2">
                <button 
                  @click="vuexStore.commit('increment')"
                  class="rounded bg-indigo-500/20 px-3 py-1 text-xs text-indigo-300 hover:bg-indigo-500/30"
                >
                  INCREMENT
                </button>
                <button 
                  @click="vuexStore.commit('decrement')"
                  class="rounded bg-indigo-500/20 px-3 py-1 text-xs text-indigo-300 hover:bg-indigo-500/30"
                >
                  DECREMENT
                </button>
                <button 
                  @click="vuexStore.commit('reset')"
                  class="rounded bg-indigo-500/20 px-3 py-1 text-xs text-indigo-300 hover:bg-indigo-500/30"
                >
                  RESET
                </button>
              </div>
            </div>
            
            <div>
              <p class="mb-2 text-xs text-gray-400">Actions (Asynchronous)</p>
              <div class="flex flex-wrap gap-2">
                <button 
                  @click="vuexStore.dispatch('incrementAsync')"
                  class="rounded bg-purple-500/20 px-3 py-1 text-xs text-purple-300 hover:bg-purple-500/30"
                  :disabled="vuexStore.state.isLoading"
                >
                  INCREMENT ASYNC
                </button>
                <button 
                  @click="vuexStore.dispatch('fetchRandomNumber')"
                  class="rounded bg-purple-500/20 px-3 py-1 text-xs text-purple-300 hover:bg-purple-500/30"
                  :disabled="vuexStore.state.isLoading"
                >
                  FETCH RANDOM
                </button>
              </div>
            </div>
          </div>
        </div>
        
        <!-- State Flow Diagram -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Vuex Flow</h4>
          <div class="grid grid-cols-2 gap-4 sm:grid-cols-4">
            <div class="rounded border border-indigo-500 bg-indigo-500/10 p-2 text-center">
              <div class="text-sm font-medium text-indigo-400">State</div>
              <div class="mt-1 text-xs text-gray-400">Single source of truth</div>
            </div>
            <div class="rounded border border-indigo-500 bg-indigo-500/10 p-2 text-center">
              <div class="text-sm font-medium text-indigo-400">Mutations</div>
              <div class="mt-1 text-xs text-gray-400">Synchronous changes</div>
            </div>
            <div class="rounded border border-purple-500 bg-purple-500/10 p-2 text-center">
              <div class="text-sm font-medium text-purple-400">Actions</div>
              <div class="mt-1 text-xs text-gray-400">Async operations</div>
            </div>
            <div class="rounded border border-indigo-500 bg-indigo-500/10 p-2 text-center">
              <div class="text-sm font-medium text-indigo-400">Getters</div>
              <div class="mt-1 text-xs text-gray-400">Computed state</div>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Pinia Section -->
    <section v-if="activeSection === 'pinia'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Pinia</h2>
      
      <div class="mx-auto max-w-3xl rounded-lg border border-yellow-500/30 bg-yellow-500/5 p-6">
        <div class="mb-6 flex items-center justify-between">
          <h3 class="text-xl font-semibold text-yellow-400">Pinia Store Simulation</h3>
          <span class="rounded-full bg-yellow-500/20 px-3 py-1 text-xs text-yellow-300">
            Store: Counter
          </span>
        </div>
        
        <!-- State & Getters Display -->
        <div class="mb-6 grid gap-6 md:grid-cols-2">
          <div class="rounded-lg border border-gray-700 bg-gray-800 p-4">
            <h4 class="mb-2 text-sm font-medium text-white">Store State</h4>
            <div class="space-y-2">
              <div class="flex items-center justify-between">
                <span class="text-xs text-gray-400">count:</span>
                <span class="text-sm font-mono text-white">{{ piniaStore.count }}</span>
              </div>
              <div class="flex items-center justify-between">
                <span class="text-xs text-gray-400">lastUpdated:</span>
                <span class="text-sm font-mono text-white">{{ piniaStore.lastUpdated }}</span>
              </div>
            </div>
          </div>
          
          <div class="rounded-lg border border-gray-700 bg-gray-800 p-4">
            <h4 class="mb-2 text-sm font-medium text-white">Getters</h4>
            <div class="space-y-2">
              <div class="flex items-center justify-between">
                <span class="text-xs text-gray-400">doubleCount:</span>
                <span class="text-sm font-mono text-white">{{ piniaStore.doubleCount }}</span>
              </div>
              <div class="flex items-center justify-between">
                <span class="text-xs text-gray-400">countStatus:</span>
                <span class="rounded bg-gray-700 px-2 py-0.5 text-xs text-white">
                  {{ piniaStore.countStatus }}
                </span>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Controls -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Actions</h4>
          <div class="grid gap-4 md:grid-cols-2">
            <div>
              <p class="mb-2 text-xs text-gray-400">Synchronous Actions</p>
              <div class="flex flex-wrap gap-2">
                <button 
                  @click="piniaStore.increment()"
                  class="rounded bg-yellow-500/20 px-3 py-1 text-xs text-yellow-300 hover:bg-yellow-500/30"
                >
                  increment()
                </button>
                <button 
                  @click="piniaStore.decrement()"
                  class="rounded bg-yellow-500/20 px-3 py-1 text-xs text-yellow-300 hover:bg-yellow-500/30"
                >
                  decrement()
                </button>
                <button 
                  @click="piniaStore.reset()"
                  class="rounded bg-yellow-500/20 px-3 py-1 text-xs text-yellow-300 hover:bg-yellow-500/30"
                >
                  reset()
                </button>
              </div>
            </div>
            
            <div>
              <p class="mb-2 text-xs text-gray-400">Asynchronous Actions</p>
              <div class="flex flex-wrap gap-2">
                <button 
                  @click="piniaStore.incrementAsync()"
                  class="rounded bg-yellow-500/20 px-3 py-1 text-xs text-yellow-300 hover:bg-yellow-500/30"
                  :disabled="piniaStore.isLoading"
                >
                  incrementAsync()
                </button>
                <button 
                  @click="piniaStore.fetchRandomNumber()"
                  class="rounded bg-yellow-500/20 px-3 py-1 text-xs text-yellow-300 hover:bg-yellow-500/30"
                  :disabled="piniaStore.isLoading"
                >
                  fetchRandomNumber()
                </button>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Pinia Code Example -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Pinia Store Definition</h4>
          <pre class="overflow-x-auto rounded bg-gray-800 p-4 text-xs text-gray-300"><code>import { defineStore } from 'pinia'
import { ref, computed } from 'vue'

export const useCounterStore = defineStore('counter', () => {
  // State
  const count = ref(0)
  const lastUpdated = ref(new Date())
  const isLoading = ref(false)

  // Getters
  const doubleCount = computed(() => count.value * 2)
  const countStatus = computed(() => {
    if (count.value &gt; 10) return 'High'
    if (count.value &lt; 0) return 'Low'
    return 'Normal'
  })

  // Actions
  function increment() {
    count.value++
    lastUpdated.value = new Date()
  }

  async function incrementAsync() {
    isLoading.value = true
    await new Promise(resolve => setTimeout(resolve, 1000))
    increment()
    isLoading.value = false
  }

  return { 
    count, lastUpdated, isLoading,
    doubleCount, countStatus,
    increment, incrementAsync
  }
})</code></pre>
        </div>
      </div>
    </section>
    
    <!-- Comparison Section -->
    <section v-if="activeSection === 'comparison'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Vuex vs Pinia</h2>
      
      <div class="mx-auto max-w-3xl overflow-x-auto rounded-lg border border-gray-700">
        <table class="w-full text-left text-sm text-gray-300">
          <thead class="bg-gray-800 text-xs uppercase text-gray-400">
            <tr>
              <th scope="col" class="p-4">Feature</th>
              <th scope="col" class="p-4 text-indigo-400">Vuex</th>
              <th scope="col" class="p-4 text-yellow-400">Pinia</th>
            </tr>
          </thead>
          <tbody>
            <tr class="border-b border-gray-700">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">API Style</th>
              <td class="p-4">Object-based with clear distinctions between state, mutations, actions, getters</td>
              <td class="p-4">Simpler, more intuitive with Options API or Composition API syntax</td>
            </tr>
            <tr class="border-b border-gray-700 bg-gray-800/30">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">TypeScript Support</th>
              <td class="p-4">Limited, requires additional setup</td>
              <td class="p-4">Excellent, built-in TypeScript support</td>
            </tr>
            <tr class="border-b border-gray-700">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">Module Structure</th>
              <td class="p-4">Requires namespaced modules</td>
              <td class="p-4">Stores are standalone by default</td>
            </tr>
            <tr class="border-b border-gray-700 bg-gray-800/30">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">Mutations</th>
              <td class="p-4">Required for state changes</td>
              <td class="p-4">No mutations, direct state changes allowed</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, computed } from 'vue';

// Section navigation
const sections = [
  { id: 'vuex', name: 'Vuex' },
  { id: 'pinia', name: 'Pinia' },
  { id: 'comparison', name: 'Comparison' }
];
const activeSection = ref('vuex');

// Vuex Store Simulation
const vuexStore = reactive({
  state: {
    count: 0,
    lastUpdated: new Date(),
    isLoading: false
  },
  getters: {
    doubleCount: computed(() => vuexStore.state.count * 2),
    countStatus: computed(() => {
      if (vuexStore.state.count > 10) return 'High';
      if (vuexStore.state.count < 0) return 'Low';
      return 'Normal';
    })
  },
  commit(type: string, payload?: any) {
    switch (type) {
      case 'increment':
        vuexStore.state.count++;
        vuexStore.state.lastUpdated = new Date();
        break;
      case 'decrement':
        vuexStore.state.count--;
        vuexStore.state.lastUpdated = new Date();
        break;
      case 'reset':
        vuexStore.state.count = 0;
        vuexStore.state.lastUpdated = new Date();
        break;
      case 'setValue':
        vuexStore.state.count = payload;
        vuexStore.state.lastUpdated = new Date();
        break;
      case 'setLoading':
        vuexStore.state.isLoading = payload;
        break;
    }
  },
  dispatch(type: string) {
    switch (type) {
      case 'incrementAsync':
        vuexStore.state.isLoading = true;
        setTimeout(() => {
          vuexStore.commit('increment');
          vuexStore.state.isLoading = false;
        }, 1000);
        break;
      case 'fetchRandomNumber':
        vuexStore.state.isLoading = true;
        setTimeout(() => {
          const randomNumber = Math.floor(Math.random() * 100);
          vuexStore.commit('setValue', randomNumber);
          vuexStore.state.isLoading = false;
        }, 1000);
        break;
    }
  }
});

// Pinia Store Simulation
const piniaStore = reactive({
  // State
  count: 0,
  lastUpdated: new Date(),
  isLoading: false,
  
  // Getters
  get doubleCount() {
    return this.count * 2;
  },
  get countStatus() {
    if (this.count > 10) return 'High';
    if (this.count < 0) return 'Low';
    return 'Normal';
  },
  
  // Actions
  increment() {
    this.count++;
    this.lastUpdated = new Date();
  },
  decrement() {
    this.count--;
    this.lastUpdated = new Date();
  },
  reset() {
    this.count = 0;
    this.lastUpdated = new Date();
  },
  setValue(value: number) {
    this.count = value;
    this.lastUpdated = new Date();
  },
  
  // Async Actions
  incrementAsync() {
    this.isLoading = true;
    setTimeout(() => {
      this.increment();
      this.isLoading = false;
    }, 1000);
  },
  fetchRandomNumber() {
    this.isLoading = true;
    setTimeout(() => {
      const randomNumber = Math.floor(Math.random() * 100);
      this.setValue(randomNumber);
      this.isLoading = false;
    }, 1000);
  }
});
</script> 