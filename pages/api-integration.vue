<template>
  <div class="min-h-screen bg-background p-8">
    <h1 class="mb-4 text-center text-4xl font-bold text-primary">API Integration</h1>
    <p class="mb-10 text-center text-gray-400">Using Axios and Fetch API for HTTP requests in Nuxt.js</p>
    
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
    
    <!-- Axios Section -->
    <section v-if="activeSection === 'axios'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Axios</h2>
      
      <div class="mx-auto max-w-3xl rounded-lg border border-green-500/30 bg-green-500/5 p-6">
        <div class="mb-6 flex items-center justify-between">
          <h3 class="text-xl font-semibold text-green-400">Axios HTTP Client</h3>
          <span class="rounded-full bg-green-500/20 px-3 py-1 text-xs text-green-300">
            @nuxtjs/axios
          </span>
        </div>
        
        <!-- Axios Demo -->
        <div class="mb-6 grid gap-6 md:grid-cols-2">
          <div class="rounded-lg border border-gray-700 bg-gray-800 p-4">
            <h4 class="mb-2 text-sm font-medium text-white">Request Methods</h4>
            <div class="space-y-3">
              <button 
                @click="fetchWithAxiosGet()"
                class="w-full rounded bg-green-500/20 px-3 py-2 text-sm text-green-300 hover:bg-green-500/30"
                :disabled="axiosLoading"
              >
                <span v-if="axiosLoading && axiosMethod === 'get'">Loading...</span>
                <span v-else>axios.get()</span>
              </button>
              
              <button 
                @click="fetchWithAxiosPost()"
                class="w-full rounded bg-green-500/20 px-3 py-2 text-sm text-green-300 hover:bg-green-500/30"
                :disabled="axiosLoading"
              >
                <span v-if="axiosLoading && axiosMethod === 'post'">Loading...</span>
                <span v-else>axios.post()</span>
              </button>
              
              <button 
                @click="fetchWithAxiosPut()"
                class="w-full rounded bg-green-500/20 px-3 py-2 text-sm text-green-300 hover:bg-green-500/30"
                :disabled="axiosLoading"
              >
                <span v-if="axiosLoading && axiosMethod === 'put'">Loading...</span>
                <span v-else>axios.put()</span>
              </button>
              
              <button 
                @click="fetchWithAxiosDelete()"
                class="w-full rounded bg-green-500/20 px-3 py-2 text-sm text-green-300 hover:bg-green-500/30"
                :disabled="axiosLoading"
              >
                <span v-if="axiosLoading && axiosMethod === 'delete'">Loading...</span>
                <span v-else>axios.delete()</span>
              </button>
            </div>
          </div>
          
          <div class="rounded-lg border border-gray-700 bg-gray-800 p-4">
            <h4 class="mb-2 text-sm font-medium text-white">Response</h4>
            <div v-if="axiosResponse">
              <div class="mb-1 flex items-center justify-between">
                <span class="text-xs text-gray-400">Status:</span>
                <span class="rounded bg-gray-700 px-2 py-0.5 text-xs font-mono" 
                  :class="axiosResponse.status >= 200 && axiosResponse.status < 300 ? 'text-green-300' : 'text-red-300'">
                  {{ axiosResponse.status }}
                </span>
              </div>
              <pre class="mt-2 h-40 overflow-auto rounded bg-gray-900 p-2 text-xs text-gray-300">{{ JSON.stringify(axiosResponse.data, null, 2) }}</pre>
            </div>
            <div v-else class="flex h-full items-center justify-center text-sm text-gray-500">
              No request sent yet
            </div>
          </div>
        </div>
        
        <!-- Axios Configuration -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Axios Configuration</h4>
          <pre class="overflow-x-auto rounded bg-gray-800 p-4 text-xs text-gray-300"><code>// plugins/axios.js
export default function ({ $axios, redirect }) {
  // Base URL
  $axios.setBaseURL('https://api.example.com')
  
  // Request interceptor
  $axios.onRequest(config => {
    // Add auth token
    const token = localStorage.getItem('token')
    if (token) {
      config.headers.common['Authorization'] = `Bearer ${token}`
    }
    return config
  })
  
  // Response interceptor
  $axios.onResponse(response => {
    return response
  })
  
  // Error interceptor
  $axios.onError(error => {
    const code = parseInt(error.response && error.response.status)
    if (code === 401) {
      redirect('/login')
    }
    return Promise.reject(error)
  })
}</code></pre>
        </div>
        
        <!-- Installation -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Installation & Setup</h4>
          <div class="mb-2">
            <span class="text-xs text-gray-400">1. Install dependency:</span>
            <pre class="mt-1 overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">npm install @nuxtjs/axios</pre>
          </div>
          <div class="mb-2">
            <span class="text-xs text-gray-400">2. Add to nuxt.config.js:</span>
            <pre class="mt-1 overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">{
  modules: [
    '@nuxtjs/axios',
  ],
  axios: {
    baseURL: process.env.API_URL || 'http://localhost:3000',
    credentials: true
  }
}</pre>
          </div>
          <div>
            <span class="text-xs text-gray-400">3. Usage in components:</span>
            <pre class="mt-1 overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">// Component methods
async fetchData() {
  try {
    const { data } = await this.$axios.get('/posts')
    this.posts = data
  } catch (error) {
    console.error(error)
  }
}</pre>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Fetch API Section -->
    <section v-if="activeSection === 'fetch'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Fetch API</h2>
      
      <div class="mx-auto max-w-3xl rounded-lg border border-blue-500/30 bg-blue-500/5 p-6">
        <div class="mb-6 flex items-center justify-between">
          <h3 class="text-xl font-semibold text-blue-400">Fetch API</h3>
          <span class="rounded-full bg-blue-500/20 px-3 py-1 text-xs text-blue-300">
            Built-in Browser API
          </span>
        </div>
        
        <!-- Fetch Demo -->
        <div class="mb-6 grid gap-6 md:grid-cols-2">
          <div class="rounded-lg border border-gray-700 bg-gray-800 p-4">
            <h4 class="mb-2 text-sm font-medium text-white">Request Methods</h4>
            <div class="space-y-3">
              <button 
                @click="fetchWithFetchGet()"
                class="w-full rounded bg-blue-500/20 px-3 py-2 text-sm text-blue-300 hover:bg-blue-500/30"
                :disabled="fetchLoading"
              >
                <span v-if="fetchLoading && fetchMethod === 'get'">Loading...</span>
                <span v-else>fetch() GET</span>
              </button>
              
              <button 
                @click="fetchWithFetchPost()"
                class="w-full rounded bg-blue-500/20 px-3 py-2 text-sm text-blue-300 hover:bg-blue-500/30"
                :disabled="fetchLoading"
              >
                <span v-if="fetchLoading && fetchMethod === 'post'">Loading...</span>
                <span v-else>fetch() POST</span>
              </button>
              
              <button 
                @click="fetchWithFetchPut()"
                class="w-full rounded bg-blue-500/20 px-3 py-2 text-sm text-blue-300 hover:bg-blue-500/30"
                :disabled="fetchLoading"
              >
                <span v-if="fetchLoading && fetchMethod === 'put'">Loading...</span>
                <span v-else>fetch() PUT</span>
              </button>
              
              <button 
                @click="fetchWithFetchDelete()"
                class="w-full rounded bg-blue-500/20 px-3 py-2 text-sm text-blue-300 hover:bg-blue-500/30"
                :disabled="fetchLoading"
              >
                <span v-if="fetchLoading && fetchMethod === 'delete'">Loading...</span>
                <span v-else>fetch() DELETE</span>
              </button>
            </div>
          </div>
          
          <div class="rounded-lg border border-gray-700 bg-gray-800 p-4">
            <h4 class="mb-2 text-sm font-medium text-white">Response</h4>
            <div v-if="fetchResponse">
              <div class="mb-1 flex items-center justify-between">
                <span class="text-xs text-gray-400">Status:</span>
                <span class="rounded bg-gray-700 px-2 py-0.5 text-xs font-mono" 
                  :class="fetchResponse.status >= 200 && fetchResponse.status < 300 ? 'text-green-300' : 'text-red-300'">
                  {{ fetchResponse.status }}
                </span>
              </div>
              <pre class="mt-2 h-40 overflow-auto rounded bg-gray-900 p-2 text-xs text-gray-300">{{ JSON.stringify(fetchResponse.data, null, 2) }}</pre>
            </div>
            <div v-else class="flex h-full items-center justify-center text-sm text-gray-500">
              No request sent yet
            </div>
          </div>
        </div>
        
        <!-- Fetch Examples -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Fetch API Examples</h4>
          <pre class="overflow-x-auto rounded bg-gray-800 p-4 text-xs text-gray-300"><code>// Basic GET request
fetch('https://api.example.com/posts')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error))

// POST request with JSON data
fetch('https://api.example.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    title: 'New Post',
    content: 'Post content'
  })
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error))

// Using async/await
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/posts')
    if (!response.ok) {
      throw new Error('Network response was not ok')
    }
    const data = await response.json()
    return data
  } catch (error) {
    console.error('Error:', error)
  }
}</code></pre>
        </div>
        
        <!-- Nuxt $fetch -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Nuxt 3 $fetch</h4>
          <p class="mb-3 text-xs text-gray-400">Nuxt 3 provides an enhanced fetch utility called $fetch that works both client and server side.</p>
          <pre class="overflow-x-auto rounded bg-gray-800 p-4 text-xs text-gray-300"><code>// In Nuxt 3 component or page
const { data: users } = await useFetch('/api/users')

// Using $fetch directly
const user = await $fetch('/api/users/1')

// With options
const response = await $fetch('/api/posts', {
  method: 'POST',
  body: {
    title: 'My new post',
    content: 'Post content'
  }
})

// Error handling
try {
  const data = await $fetch('/api/protected', {
    headers: {
      Authorization: `Bearer ${token}`
    }
  })
} catch (error) {
  // Handle error
}</code></pre>
        </div>
      </div>
    </section>
    
    <!-- Comparison Section -->
    <section v-if="activeSection === 'comparison'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Axios vs Fetch API</h2>
      
      <div class="mx-auto max-w-3xl overflow-x-auto rounded-lg border border-gray-700">
        <table class="w-full text-left text-sm text-gray-300">
          <thead class="bg-gray-800 text-xs uppercase text-gray-400">
            <tr>
              <th scope="col" class="p-4">Feature</th>
              <th scope="col" class="p-4 text-green-400">Axios</th>
              <th scope="col" class="p-4 text-blue-400">Fetch API</th>
            </tr>
          </thead>
          <tbody>
            <tr class="border-b border-gray-700">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">Browser Support</th>
              <td class="p-4">All browsers (uses XMLHttpRequest)</td>
              <td class="p-4">Modern browsers only (polyfill needed for older browsers)</td>
            </tr>
            <tr class="border-b border-gray-700 bg-gray-800/30">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">JSON Parsing</th>
              <td class="p-4">Automatic</td>
              <td class="p-4">Manual (.json() method)</td>
            </tr>
            <tr class="border-b border-gray-700">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">Request Cancellation</th>
              <td class="p-4">Built-in (CancelToken)</td>
              <td class="p-4">Using AbortController</td>
            </tr>
            <tr class="border-b border-gray-700 bg-gray-800/30">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">Error Handling</th>
              <td class="p-4">HTTP error status codes throw errors</td>
              <td class="p-4">HTTP error status don't throw errors (need to check response.ok)</td>
            </tr>
            <tr class="border-b border-gray-700">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">Interceptors</th>
              <td class="p-4">Built-in</td>
              <td class="p-4">Need to implement manually</td>
            </tr>
            <tr class="border-b border-gray-700 bg-gray-800/30">
              <th scope="row" class="whitespace-nowrap p-4 font-medium text-white">Request Timeout</th>
              <td class="p-4">Built-in</td>
              <td class="p-4">Need to implement manually</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue';

// Section navigation
const sections = [
  { id: 'axios', name: 'Axios' },
  { id: 'fetch', name: 'Fetch API' },
  { id: 'comparison', name: 'Comparison' }
];
const activeSection = ref('axios');

// Axios demo states
const axiosLoading = ref(false);
const axiosMethod = ref('');
const axiosResponse = ref(null);

// Fetch demo states
const fetchLoading = ref(false);
const fetchMethod = ref('');
const fetchResponse = ref(null);

// Mock API functions for Axios
async function fetchWithAxiosGet() {
  axiosLoading.value = true;
  axiosMethod.value = 'get';
  
  // Simulate API request
  await new Promise(resolve => setTimeout(resolve, 1000));
  
  axiosResponse.value = {
    status: 200,
    data: {
      id: 1,
      title: 'Sample Post',
      body: 'This is a sample post fetched with axios.get()',
      tags: ['api', 'axios', 'get']
    }
  };
  
  axiosLoading.value = false;
}

async function fetchWithAxiosPost() {
  axiosLoading.value = true;
  axiosMethod.value = 'post';
  
  // Simulate API request
  await new Promise(resolve => setTimeout(resolve, 1000));
  
  axiosResponse.value = {
    status: 201,
    data: {
      id: 101,
      title: 'New Post',
      body: 'This post was created with axios.post()',
      createdAt: new Date().toISOString()
    }
  };
  
  axiosLoading.value = false;
}

async function fetchWithAxiosPut() {
  axiosLoading.value = true;
  axiosMethod.value = 'put';
  
  // Simulate API request
  await new Promise(resolve => setTimeout(resolve, 1000));
  
  axiosResponse.value = {
    status: 200,
    data: {
      id: 1,
      title: 'Updated Post',
      body: 'This post was updated with axios.put()',
      updatedAt: new Date().toISOString()
    }
  };
  
  axiosLoading.value = false;
}

async function fetchWithAxiosDelete() {
  axiosLoading.value = true;
  axiosMethod.value = 'delete';
  
  // Simulate API request
  await new Promise(resolve => setTimeout(resolve, 1000));
  
  axiosResponse.value = {
    status: 204,
    data: {}
  };
  
  axiosLoading.value = false;
}

// Mock API functions for Fetch
async function fetchWithFetchGet() {
  fetchLoading.value = true;
  fetchMethod.value = 'get';
  
  // Simulate API request
  await new Promise(resolve => setTimeout(resolve, 1000));
  
  fetchResponse.value = {
    status: 200,
    data: {
      id: 1,
      title: 'Sample Post',
      body: 'This is a sample post fetched with fetch() GET',
      tags: ['api', 'fetch', 'get']
    }
  };
  
  fetchLoading.value = false;
}

async function fetchWithFetchPost() {
  fetchLoading.value = true;
  fetchMethod.value = 'post';
  
  // Simulate API request
  await new Promise(resolve => setTimeout(resolve, 1000));
  
  fetchResponse.value = {
    status: 201,
    data: {
      id: 101,
      title: 'New Post',
      body: 'This post was created with fetch() POST',
      createdAt: new Date().toISOString()
    }
  };
  
  fetchLoading.value = false;
}

async function fetchWithFetchPut() {
  fetchLoading.value = true;
  fetchMethod.value = 'put';
  
  // Simulate API request
  await new Promise(resolve => setTimeout(resolve, 1000));
  
  fetchResponse.value = {
    status: 200,
    data: {
      id: 1,
      title: 'Updated Post',
      body: 'This post was updated with fetch() PUT',
      updatedAt: new Date().toISOString()
    }
  };
  
  fetchLoading.value = false;
}

async function fetchWithFetchDelete() {
  fetchLoading.value = true;
  fetchMethod.value = 'delete';
  
  // Simulate API request
  await new Promise(resolve => setTimeout(resolve, 1000));
  
  fetchResponse.value = {
    status: 204,
    data: {}
  };
  
  fetchLoading.value = false;
}
</script> 