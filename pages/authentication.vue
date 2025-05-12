<template>
  <div class="min-h-screen bg-background p-8">
    <h1 class="mb-4 text-center text-4xl font-bold text-primary">Authentication</h1>
    <p class="mb-10 text-center text-gray-400">Implementing authentication in Nuxt.js with @nuxtjs/auth-next</p>
    
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
    
    <!-- Auth Setup Section -->
    <section v-if="activeSection === 'setup'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Setup & Configuration</h2>
      
      <div class="mx-auto max-w-3xl rounded-lg border border-orange-500/30 bg-orange-500/5 p-6">
        <div class="mb-6 flex items-center justify-between">
          <h3 class="text-xl font-semibold text-orange-400">Nuxt Auth Module</h3>
          <span class="rounded-full bg-orange-500/20 px-3 py-1 text-xs text-orange-300">
            @nuxtjs/auth-next
          </span>
        </div>
        
        <!-- Installation Steps -->
        <div class="mb-6 space-y-4 rounded-lg border border-gray-700 bg-gray-800 p-4">
          <div>
            <h4 class="mb-2 text-sm font-medium text-white">1. Installation</h4>
            <pre class="overflow-x-auto rounded bg-gray-900 p-3 text-xs text-gray-300">npm install --save-dev @nuxtjs/auth-next @nuxtjs/axios</pre>
          </div>
          
          <div>
            <h4 class="mb-2 text-sm font-medium text-white">2. Configure nuxt.config.js</h4>
            <pre class="overflow-x-auto rounded bg-gray-900 p-3 text-xs text-gray-300">{
  modules: [
    '@nuxtjs/axios',
    '@nuxtjs/auth-next'
  ],
  
  axios: {
    baseURL: 'https://api.example.com'
  },
  
  auth: {
    strategies: {
      local: {
        token: {
          property: 'token',
          global: true,
          required: true,
          type: 'Bearer'
        },
        user: {
          property: 'user',
          autoFetch: true
        },
        endpoints: {
          login: { url: '/api/auth/login', method: 'post' },
          logout: { url: '/api/auth/logout', method: 'post' },
          user: { url: '/api/auth/user', method: 'get' }
        }
      }
    },
    redirect: {
      login: '/login',
      logout: '/',
      callback: '/login',
      home: '/dashboard'
    }
  }
}</pre>
          </div>
          
          <div>
            <h4 class="mb-2 text-sm font-medium text-white">3. Create auth middleware</h4>
            <pre class="overflow-x-auto rounded bg-gray-900 p-3 text-xs text-gray-300">// middleware/auth.js
export default function ({ $auth, redirect }) {
  if (!$auth.loggedIn) {
    return redirect('/login')
  }
}</pre>
          </div>
        </div>
        
        <!-- Auth Strategies -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Available Authentication Strategies</h4>
          
          <div class="grid gap-4 md:grid-cols-2">
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3 transition-colors hover:bg-gray-700">
              <div class="flex items-center justify-between">
                <h5 class="text-sm font-medium text-orange-300">Local</h5>
                <span class="rounded bg-gray-700 px-2 py-0.5 text-xs text-gray-300">Username/Password</span>
              </div>
              <p class="mt-2 text-xs text-gray-400">
                Traditional email/username and password login with JWT
              </p>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3 transition-colors hover:bg-gray-700">
              <div class="flex items-center justify-between">
                <h5 class="text-sm font-medium text-orange-300">OAuth2</h5>
                <span class="rounded bg-gray-700 px-2 py-0.5 text-xs text-gray-300">Social Login</span>
              </div>
              <p class="mt-2 text-xs text-gray-400">
                Authentication with social providers (Google, Facebook, etc.)
              </p>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3 transition-colors hover:bg-gray-700">
              <div class="flex items-center justify-between">
                <h5 class="text-sm font-medium text-orange-300">Refresh</h5>
                <span class="rounded bg-gray-700 px-2 py-0.5 text-xs text-gray-300">Token Refresh</span>
              </div>
              <p class="mt-2 text-xs text-gray-400">
                JWT with automatic token refresh
              </p>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3 transition-colors hover:bg-gray-700">
              <div class="flex items-center justify-between">
                <h5 class="text-sm font-medium text-orange-300">Laravel Sanctum</h5>
                <span class="rounded bg-gray-700 px-2 py-0.5 text-xs text-gray-300">Laravel</span>
              </div>
              <p class="mt-2 text-xs text-gray-400">
                Authentication for Laravel-based backends using Sanctum
              </p>
            </div>
          </div>
        </div>
        
        <!-- Router Config -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Page Middleware Configuration</h4>
          <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">// pages/dashboard.vue
export default {
  middleware: ['auth'],
  // ...
}

// In pages/admin/index.vue
export default {
  middleware: ['auth', 'admin'],  // Use multiple middleware
  // ...
}

// For multiple pages, set it in nuxt.config.js
router: {
  middleware: ['auth']
}</pre>
        </div>
      </div>
    </section>
    
    <!-- Auth Usage Section -->
    <section v-if="activeSection === 'usage'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Usage & Methods</h2>
      
      <div class="mx-auto max-w-3xl rounded-lg border border-orange-500/30 bg-orange-500/5 p-6">
        <!-- Auth Demo -->
        <div class="mb-6 grid gap-6 md:grid-cols-2">
          <div class="rounded-lg border border-gray-700 bg-gray-800 p-4">
            <h4 class="mb-4 text-sm font-medium text-white">Auth State Demo</h4>
            
            <div class="mb-4 rounded-lg border border-gray-700 bg-gray-900 p-3">
              <div class="flex items-center justify-between">
                <h5 class="text-xs font-medium text-orange-300">Current Status</h5>
                <span 
                  class="rounded px-2 py-0.5 text-xs font-medium"
                  :class="isAuthenticated ? 'bg-green-500/20 text-green-300' : 'bg-red-500/20 text-red-300'"
                >
                  {{ isAuthenticated ? 'Authenticated' : 'Not Authenticated' }}
                </span>
              </div>
              
              <div v-if="isAuthenticated" class="mt-3 space-y-2">
                <div class="flex items-center justify-between">
                  <span class="text-xs text-gray-400">User ID:</span>
                  <span class="font-mono text-xs text-gray-300">{{ authUser.id }}</span>
                </div>
                <div class="flex items-center justify-between">
                  <span class="text-xs text-gray-400">Username:</span>
                  <span class="font-mono text-xs text-gray-300">{{ authUser.username }}</span>
                </div>
                <div class="flex items-center justify-between">
                  <span class="text-xs text-gray-400">Email:</span>
                  <span class="font-mono text-xs text-gray-300">{{ authUser.email }}</span>
                </div>
                <div class="flex items-center justify-between">
                  <span class="text-xs text-gray-400">Role:</span>
                  <span class="rounded bg-orange-500/20 px-2 py-0.5 text-xs text-orange-300">{{ authUser.role }}</span>
                </div>
              </div>
            </div>
            
            <div class="space-y-2">
              <button 
                v-if="!isAuthenticated"
                @click="login"
                class="w-full rounded bg-orange-500/20 px-3 py-2 text-sm text-orange-300 hover:bg-orange-500/30"
              >
                Log In
              </button>
              
              <button 
                v-else
                @click="logout"
                class="w-full rounded bg-red-500/20 px-3 py-2 text-sm text-red-300 hover:bg-red-500/30"
              >
                Log Out
              </button>
              
              <button 
                @click="fetchUser"
                class="w-full rounded bg-gray-700 px-3 py-2 text-sm text-gray-300 hover:bg-gray-600"
                :disabled="!isAuthenticated"
              >
                Refresh User Data
              </button>
            </div>
          </div>
          
          <div class="rounded-lg border border-gray-700 bg-gray-800 p-4">
            <h4 class="mb-4 text-sm font-medium text-white">Auth Methods</h4>
            <div class="space-y-4">
              <div>
                <h5 class="text-xs font-medium text-orange-300">Authentication</h5>
                <pre class="mt-1 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">// Login
await this.$auth.loginWith('local', {
  data: {
    email: 'user@example.com',
    password: 'password123'
  }
})

// Logout
await this.$auth.logout()

// Check if authenticated
const isLoggedIn = this.$auth.loggedIn

// Get current user
const user = this.$auth.user</pre>
              </div>
              
              <div>
                <h5 class="text-xs font-medium text-orange-300">Token Handling</h5>
                <pre class="mt-1 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">// Get token
const token = this.$auth.strategy.token.get()

// Set token manually
this.$auth.strategy.token.set('YOUR_TOKEN')

// Access token expiration
const exp = this.$auth.strategy.token.status().expiresIn</pre>
              </div>
              
              <div>
                <h5 class="text-xs font-medium text-orange-300">Social Login</h5>
                <pre class="mt-1 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">// Login with Google
this.$auth.loginWith('google')

// Login with Facebook
this.$auth.loginWith('facebook')</pre>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Auth Login Component -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Login Component Example</h4>
          <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">&lt;template&gt;
  &lt;form @submit.prevent="login"&gt;
    &lt;div class="form-group"&gt;
      &lt;label&gt;Email&lt;/label&gt;
      &lt;input v-model="email" type="email" required /&gt;
    &lt;/div&gt;
    
    &lt;div class="form-group"&gt;
      &lt;label&gt;Password&lt;/label&gt;
      &lt;input v-model="password" type="password" required /&gt;
    &lt;/div&gt;
    
    &lt;div v-if="error" class="error"&gt;
      {{ error }}
    &lt;/div&gt;
    
    &lt;button type="submit" :disabled="loading"&gt;
      {{ loading ? 'Logging in...' : 'Login' }}
    &lt;/button&gt;
  &lt;/form&gt;
&lt;/template&gt;

&lt;script&gt;
export default {
  auth: 'guest', // Only accessible if not logged in
  data() {
    return {
      email: '',
      password: '',
      error: null,
      loading: false
    }
  },
  methods: {
    async login() {
      this.error = null
      this.loading = true
      
      try {
        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          }
        })
        // Redirect is handled automatically by the module
      } catch (e) {
        this.error = e.response?.data?.message || 'Login failed'
      } finally {
        this.loading = false
      }
    }
  }
}
&lt;/script&gt;</pre>
        </div>
        
        <!-- Auth Guards -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Auth Guards in Components</h4>
          <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">&lt;template&gt;
  &lt;div&gt;
    &lt;!-- Content visible to everyone --&gt;
    &lt;div&gt;Public content&lt;/div&gt;
    
    &lt;!-- Only visible when authenticated --&gt;
    &lt;div v-if="$auth.loggedIn"&gt;
      Welcome, &#123;&#123; $auth.user.name &#125;&#125;!
      &lt;button @click="$auth.logout()"&gt;Logout&lt;/button&gt;
    &lt;/div&gt;
    
    &lt;!-- Only visible when not authenticated --&gt;
    &lt;div v-else&gt;
      &lt;nuxt-link to="/login"&gt;Login&lt;/nuxt-link&gt;
      &lt;nuxt-link to="/register"&gt;Register&lt;/nuxt-link&gt;
    &lt;/div&gt;
    
    &lt;!-- Only visible for admin users --&gt;
    &lt;div v-if="$auth.loggedIn && $auth.user.role === 'admin'"&gt;
      Admin Panel
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/template&gt;</pre>
        </div>
      </div>
    </section>
    
    <!-- Auth Best Practices -->
    <section v-if="activeSection === 'best-practices'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Best Practices</h2>
      
      <div class="mx-auto max-w-3xl rounded-lg border border-orange-500/30 bg-orange-500/5 p-6">
        <!-- Security Best Practices -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-4 text-sm font-medium text-white">Security Best Practices</h4>
          
          <div class="space-y-4">
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-sm font-medium text-orange-300">Use HTTPS</h5>
              <p class="mt-1 text-xs text-gray-400">
                Always use HTTPS for production environments to prevent token interception.
              </p>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-sm font-medium text-orange-300">Token Storage</h5>
              <p class="mt-1 text-xs text-gray-400">
                For most applications, use the default cookie storage. For high-security apps, consider using HttpOnly cookies.
              </p>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-sm font-medium text-orange-300">Refresh Tokens</h5>
              <p class="mt-1 text-xs text-gray-400">
                Implement token refresh for long user sessions. Configure short-lived access tokens with longer refresh tokens.
              </p>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-sm font-medium text-orange-300">Role-Based Access</h5>
              <p class="mt-1 text-xs text-gray-400">
                Implement proper role checks both on the frontend (UI access) and backend (API protection).
              </p>
            </div>
          </div>
        </div>
        
        <!-- Implementation Patterns -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-4 text-sm font-medium text-white">Auth Implementation Patterns</h4>
          
          <div class="space-y-4">
            <div>
              <h5 class="mb-2 text-xs font-medium text-orange-300">1. Custom auth middleware for roles</h5>
              <pre class="overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">// middleware/admin.js
export default function ({ $auth, redirect }) {
  // Check if user is authenticated and has admin role
  if (!$auth.loggedIn || $auth.user.role !== 'admin') {
    return redirect('/unauthorized')
  }
}</pre>
            </div>
            
            <div>
              <h5 class="mb-2 text-xs font-medium text-orange-300">2. Automatic token refresh</h5>
              <pre class="overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">// nuxt.config.js
auth: {
  strategies: {
    local: {
      token: {
        maxAge: 1800 // 30 minutes
      },
      refreshToken: {
        maxAge: 60 * 60 * 24 * 30 // 30 days
      }
    }
  }
}</pre>
            </div>
            
            <div>
              <h5 class="mb-2 text-xs font-medium text-orange-300">3. Custom callback handling</h5>
              <pre class="overflow-x-auto rounded bg-gray-800 p-2 text-xs text-gray-300">// For OAuth providers
// pages/login/callback.vue
export default {
  auth: false,
  async mounted() {
    await this.$auth.fetchUser()
    // Do something after login
    return this.$router.push('/dashboard')
  }
}</pre>
            </div>
          </div>
        </div>
        
        <!-- Common Patterns -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Authentication Flow Diagram</h4>
          
          <div class="flex justify-center">
            <div class="relative mt-4 h-80 w-full max-w-lg rounded bg-gray-800 p-4">
              <!-- Boxes -->
              <div class="absolute left-1/2 top-6 h-14 w-36 -translate-x-1/2 transform rounded bg-orange-500/20 p-2 text-center text-xs font-medium text-orange-300">
                Login Form
              </div>
              
              <div class="absolute left-1/2 top-32 h-14 w-36 -translate-x-1/2 transform rounded bg-blue-500/20 p-2 text-center text-xs font-medium text-blue-300">
                Auth Module
              </div>
              
              <div class="absolute left-1/4 top-52 h-14 w-32 -translate-x-1/2 transform rounded bg-green-500/20 p-2 text-center text-xs font-medium text-green-300">
                API Server
              </div>
              
              <div class="absolute left-3/4 top-52 h-14 w-32 -translate-x-1/2 transform rounded bg-purple-500/20 p-2 text-center text-xs font-medium text-purple-300">
                Store Token
              </div>
              
              <div class="absolute bottom-6 left-1/2 h-14 w-36 -translate-x-1/2 transform rounded bg-teal-500/20 p-2 text-center text-xs font-medium text-teal-300">
                Dashboard
              </div>
              
              <!-- Arrows -->
              <svg class="absolute inset-0 h-full w-full" xmlns="http://www.w3.org/2000/svg">
                <line x1="50%" y1="20" x2="50%" y2="32" stroke="#f97316" stroke-width="1" stroke-dasharray="4" />
                <line x1="50%" y1="46" x2="50%" y2="58" stroke="#3b82f6" stroke-width="1" stroke-dasharray="4" />
                <line x1="50%" y1="46" x2="25%" y2="52" stroke="#3b82f6" stroke-width="1" stroke-dasharray="4" />
                <line x1="25%" y1="66" x2="50%" y2="78" stroke="#10b981" stroke-width="1" stroke-dasharray="4" />
                <line x1="50%" y1="46" x2="75%" y2="52" stroke="#3b82f6" stroke-width="1" stroke-dasharray="4" />
                <line x1="75%" y1="66" x2="50%" y2="78" stroke="#8b5cf6" stroke-width="1" stroke-dasharray="4" />
              </svg>
              
              <div class="absolute bottom-4 left-0 right-0 text-center text-xs text-gray-400">
                Standard Authentication Flow
              </div>
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
  { id: 'setup', name: 'Setup & Configuration' },
  { id: 'usage', name: 'Usage & Methods' },
  { id: 'best-practices', name: 'Best Practices' }
];
const activeSection = ref('setup');

// Simulated authentication state
const isAuthenticated = ref(false);
const authUser = reactive({
  id: 'usr_123456',
  username: 'demo_user',
  email: 'user@example.com',
  role: 'admin'
});

// Auth methods
function login() {
  isAuthenticated.value = true;
  // In a real app, this would call $auth.loginWith()
}

function logout() {
  isAuthenticated.value = false;
  // In a real app, this would call $auth.logout()
}

function fetchUser() {
  // In a real app, this would call $auth.fetchUser()
  console.log('Fetching user data...');
  // Mock data refresh
  setTimeout(() => {
    authUser.lastLogin = new Date().toISOString();
  }, 500);
}
</script>