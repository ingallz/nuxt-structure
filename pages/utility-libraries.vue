<template>
  <div class="min-h-screen bg-background p-8">
    <h1 class="mb-4 text-center text-4xl font-bold text-primary">Utility Libraries</h1>
    <p class="mb-10 text-center text-gray-400">Common utility libraries for Nuxt.js applications</p>
    
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
    
    <!-- Lodash Section -->
    <section v-if="activeSection === 'lodash'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Lodash</h2>
      
      <div class="mx-auto max-w-3xl rounded-lg border border-blue-500/30 bg-blue-500/5 p-6">
        <div class="mb-6 flex items-center justify-between">
          <h3 class="text-xl font-semibold text-blue-400">Lodash Utilities</h3>
          <span class="rounded-full bg-blue-500/20 px-3 py-1 text-xs text-blue-300">
            Performance & Safety
          </span>
        </div>
        
        <!-- Lodash Installation -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-800 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Installation</h4>
          <pre class="overflow-x-auto rounded bg-gray-900 p-3 text-xs text-gray-300">npm install lodash
# For TypeScript
npm install @types/lodash --save-dev

# Import in component
import _ from 'lodash'
// Or import specific functions
import { debounce, throttle } from 'lodash'</pre>
        </div>
        
        <!-- Performance Optimization -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Performance Optimization</h4>
          
          <div class="mb-4">
            <h5 class="mb-2 text-xs font-medium text-blue-300">_.debounce()</h5>
            <p class="mb-2 text-xs text-gray-400">
              Creates a debounced function that delays invoking the function until after a specified wait time.
            </p>
            <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">// Execute search only after user stops typing for 300ms
const debouncedSearch = _.debounce(function(query) {
  searchAPI(query);
}, 300);

// In a Vue component
&lt;input 
  type="text" 
  v-model="searchQuery" 
  @input="debouncedSearch(searchQuery)" 
/&gt;</pre>
          </div>
          
          <div>
            <h5 class="mb-2 text-xs font-medium text-blue-300">_.throttle()</h5>
            <p class="mb-2 text-xs text-gray-400">
              Creates a throttled function that only invokes the function at most once per every wait milliseconds.
            </p>
            <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">// Handle resize events at most once every 200ms
const throttledResize = _.throttle(function() {
  updateLayout();
}, 200);

// In Vue component's mounted hook
window.addEventListener('resize', throttledResize);

// Don't forget to remove it
onBeforeUnmount(() => {
  window.removeEventListener('resize', throttledResize);
});</pre>
          </div>
        </div>
        
        <!-- Safe Object Access -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Safe Object Access</h4>
          
          <div class="mb-4">
            <h5 class="mb-2 text-xs font-medium text-blue-300">_.get()</h5>
            <p class="mb-2 text-xs text-gray-400">
              Gets the value at path of object. If the resolved value is undefined, the defaultValue is returned.
            </p>
            <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">const user = {
  profile: {
    name: 'John',
    address: {
      city: 'New York'
    }
  }
};

// Without lodash - prone to errors if properties don't exist
const city = user.profile.address.city; // Error if address is undefined

// With lodash - safe access
const city = _.get(user, 'profile.address.city', 'Unknown');
// Returns 'New York' or 'Unknown' if path doesn't exist</pre>
          </div>
          
          <div>
            <h5 class="mb-2 text-xs font-medium text-blue-300">_.set()</h5>
            <p class="mb-2 text-xs text-gray-400">
              Sets the value at path of object. If a portion of path doesn't exist, it's created.
            </p>
            <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">const user = {};

// Without lodash - error if intermediate objects don't exist
user.profile.address.city = 'New York'; // Error!

// With lodash - safely sets values, creating intermediate objects
_.set(user, 'profile.address.city', 'New York');
// Result: { profile: { address: { city: 'New York' } } }</pre>
          </div>
        </div>
        
        <!-- Collection Manipulation -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Collection Manipulation</h4>
          
          <div class="grid gap-4 md:grid-cols-2">
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-blue-300">_.filter() & _.find()</h5>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">// Filter active users
const activeUsers = _.filter(users, { active: true });

// Find first admin user
const admin = _.find(users, { role: 'admin' });</pre>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-blue-300">_.groupBy()</h5>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">// Group users by role
const usersByRole = _.groupBy(users, 'role');
// { admin: [...], user: [...], guest: [...] }</pre>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-blue-300">_.sortBy() & _.orderBy()</h5>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">// Sort by age ascending
const sortedByAge = _.sortBy(users, 'age');

// Sort by multiple properties
const sorted = _.orderBy(users, 
  ['active', 'name'], 
  ['desc', 'asc']);</pre>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-blue-300">_.uniqBy() & _.merge()</h5>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">// Unique users by ID
const uniqueUsers = _.uniqBy(users, 'id');

// Deep merge objects
const mergedConfig = _.merge(defaultConfig, userConfig);</pre>
            </div>
          </div>
        </div>
        
        <!-- Lodash FP -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Functional Programming with Lodash FP</h4>
          <p class="mb-3 text-xs text-gray-400">
            Lodash FP provides a more functional approach with auto-curried and immutable functions.
          </p>
          <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">import fp from 'lodash/fp';

// Create a processing pipeline
const processData = fp.flow(
  fp.filter(user => user.active),
  fp.map(fp.pick(['id', 'name', 'email'])),
  fp.sortBy('name')
);

// Apply the pipeline to data
const processedUsers = processData(users);</pre>
        </div>
      </div>
    </section>
    
    <!-- Date Libraries Section -->
    <section v-if="activeSection === 'date-libraries'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Date Libraries</h2>
      
      <div class="mx-auto max-w-3xl rounded-lg border border-green-500/30 bg-green-500/5 p-6">
        <div class="mb-6 flex items-center justify-between">
          <h3 class="text-xl font-semibold text-green-400">Date & Time Manipulation</h3>
          <div class="flex gap-2">
            <span class="rounded-full bg-green-500/20 px-3 py-1 text-xs text-green-300">
              Moment.js
            </span>
            <span class="rounded-full bg-green-500/20 px-3 py-1 text-xs text-green-300">
              Day.js
            </span>
          </div>
        </div>
        
        <!-- Moment.js -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <div class="mb-3 flex items-center justify-between">
            <h4 class="text-sm font-medium text-white">Moment.js</h4>
            <span class="rounded bg-yellow-500/20 px-2 py-0.5 text-xs text-yellow-300">
              Legacy but popular
            </span>
          </div>
          
          <div class="mb-3">
            <p class="text-xs text-gray-400">
              Note: While still widely used, Moment.js is now considered legacy. For new projects, consider Day.js, date-fns, or Luxon.
            </p>
          </div>
          
          <div class="mb-3">
            <h5 class="mb-2 text-xs font-medium text-green-300">Installation</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">npm install moment

// Import in component
import moment from 'moment'</pre>
          </div>
          
          <div class="mb-3">
            <h5 class="mb-2 text-xs font-medium text-green-300">Formatting Dates</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">// Current date in different formats
moment().format('YYYY-MM-DD') // "2023-06-15"
moment().format('DD/MM/YYYY') // "15/06/2023"
moment().format('MMMM Do, YYYY') // "June 15th, 2023"
moment().format('ddd, hA') // "Thu, 3PM"

// Parse specific date
moment('2023-06-15').format('DD MMM YYYY') // "15 Jun 2023"</pre>
          </div>
          
          <div class="mb-3">
            <h5 class="mb-2 text-xs font-medium text-green-300">Time Differences</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">// Get difference between dates
const a = moment('2023-01-01')
const b = moment('2023-06-15')

b.diff(a, 'days') // 165
b.diff(a, 'months') // 5
b.diff(a, 'years', true) // 0.45...

// Human readable difference
moment('2023-06-15').fromNow() // "2 months ago"
moment('2023-08-20').from(moment('2023-06-15')) // "in 2 months"</pre>
          </div>
          
          <div>
            <h5 class="mb-2 text-xs font-medium text-green-300">Manipulating Dates</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">// Add time
moment().add(1, 'days') // tomorrow
moment().add(3, 'months') // 3 months from now

// Subtract time
moment().subtract(7, 'days') // a week ago

// Start/end of periods
moment().startOf('month') // first day of current month
moment().endOf('year') // last day of current year

// Check relationship
moment('2023-06-15').isBefore('2023-06-16') // true
moment('2023-06-15').isAfter('2023-06-14') // true
moment('2023-06-15').isSame('2023-06-15') // true</pre>
          </div>
        </div>
        
        <!-- Day.js -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <div class="mb-3 flex items-center justify-between">
            <h4 class="text-sm font-medium text-white">Day.js</h4>
            <span class="rounded bg-green-500/20 px-2 py-0.5 text-xs text-green-300">
              Modern alternative
            </span>
          </div>
          
          <div class="mb-3">
            <p class="text-xs text-gray-400">
              Day.js is a minimalist JavaScript library that parses, validates, manipulates, and displays dates and times. It offers a Moment.js-compatible API but is much smaller (2KB vs 300KB+).
            </p>
          </div>
          
          <div class="mb-3">
            <h5 class="mb-2 text-xs font-medium text-green-300">Installation</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">npm install dayjs

// Import in component
import dayjs from 'dayjs'

// Optional plugins
import relativeTime from 'dayjs/plugin/relativeTime'
dayjs.extend(relativeTime)</pre>
          </div>
          
          <div class="mb-3">
            <h5 class="mb-2 text-xs font-medium text-green-300">API Comparison with Moment.js</h5>
            <pre class="overflow-x-auto rounded bg-gray-800 p-3 text-xs text-gray-300">// Formatting
dayjs().format('YYYY-MM-DD') // same as moment

// Adding time
dayjs().add(1, 'day') // same as moment

// Difference
dayjs('2023-06-15').diff(dayjs('2023-01-01'), 'month') // same as moment

// Relative time (with plugin)
dayjs('2023-06-15').fromNow() // same as moment</pre>
          </div>
        </div>
        
        <!-- Other Date Libraries -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-4">
          <h4 class="mb-3 text-sm font-medium text-white">Other Date Libraries</h4>
          
          <div class="grid gap-4 md:grid-cols-2">
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-green-300">date-fns</h5>
              <p class="mt-2 text-xs text-gray-400">
                Functional approach to date manipulation with tree-shakeable modules.
              </p>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">import { format, addDays } from 'date-fns'

format(new Date(), 'yyyy-MM-dd')
addDays(new Date(), 1)</pre>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-green-300">Luxon</h5>
              <p class="mt-2 text-xs text-gray-400">
                A powerful, modern library for handling dates and times.
              </p>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">import { DateTime } from 'luxon'

DateTime.now().toFormat('yyyy-MM-dd')
DateTime.now().plus({ days: 1 })</pre>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Other Libraries Section -->
    <section v-if="activeSection === 'other-libraries'" class="mt-8">
      <h2 class="mb-6 text-center text-2xl font-bold text-white">Other Useful Libraries</h2>
      
      <div class="mx-auto max-w-3xl rounded-lg border border-purple-500/30 bg-purple-500/5 p-6">
        <!-- Form Validation -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <div class="mb-3 flex items-center justify-between">
            <h4 class="text-sm font-medium text-white">Form Validation</h4>
            <div class="flex gap-2">
              <span class="rounded-full bg-purple-500/20 px-3 py-1 text-xs text-purple-300">
                Vuelidate
              </span>
              <span class="rounded-full bg-purple-500/20 px-3 py-1 text-xs text-purple-300">
                Yup
              </span>
            </div>
          </div>
          
          <div class="grid gap-4 md:grid-cols-2">
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-purple-300">Vuelidate</h5>
              <p class="mt-2 text-xs text-gray-400">
                A model-based validation library for Vue.js that is extensible and supports async validation.
              </p>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">import { useVuelidate } from '@vuelidate/core'
import { required, email, minLength } from '@vuelidate/validators'

const rules = {
  name: { required },
  email: { required, email },
  password: { required, minLength: minLength(8) }
}</pre>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-purple-300">Yup / Zod</h5>
              <p class="mt-2 text-xs text-gray-400">
                Schema-based validation libraries that work well with forms.
              </p>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">import * as yup from 'yup';

const schema = yup.object().shape({
  name: yup.string().required(),
  email: yup.string().email().required(),
  password: yup.string().min(8).required()
});</pre>
            </div>
          </div>
        </div>
        
        <!-- HTTP Libraries -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <div class="mb-3 flex items-center justify-between">
            <h4 class="text-sm font-medium text-white">HTTP & API</h4>
            <div class="flex gap-2">
              <span class="rounded-full bg-purple-500/20 px-3 py-1 text-xs text-purple-300">
                Axios
              </span>
              <span class="rounded-full bg-purple-500/20 px-3 py-1 text-xs text-purple-300">
                SWR
              </span>
            </div>
          </div>
          
          <div class="grid gap-4 md:grid-cols-2">
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-purple-300">Axios</h5>
              <p class="mt-2 text-xs text-gray-400">
                Promise-based HTTP client with request/response interceptors.
              </p>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">import axios from 'axios'

// Global axios config
axios.defaults.baseURL = 'https://api.example.com'
axios.defaults.headers.common['Authorization'] = token

// Request with interceptors
axios.interceptors.request.use(config => {
  // Modify request before sending
  return config
})</pre>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-purple-300">SWR / Vue Query</h5>
              <p class="mt-2 text-xs text-gray-400">
                Data fetching libraries with caching, revalidation, and more.
              </p>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">// Vue Query example
import { useQuery } from '@tanstack/vue-query'

const { isLoading, error, data } = useQuery({
  queryKey: ['todos'],
  queryFn: fetchTodos,
  staleTime: 60000 // 1 minute
})</pre>
            </div>
          </div>
        </div>
        
        <!-- Utils & Formatters -->
        <div class="mb-6 rounded-lg border border-gray-700 bg-gray-900 p-4">
          <div class="mb-3 flex items-center justify-between">
            <h4 class="text-sm font-medium text-white">Utils & Formatters</h4>
            <div class="flex gap-2">
              <span class="rounded-full bg-purple-500/20 px-3 py-1 text-xs text-purple-300">
                NumericJS
              </span>
              <span class="rounded-full bg-purple-500/20 px-3 py-1 text-xs text-purple-300">
                Currency.js
              </span>
            </div>
          </div>
          
          <div class="grid gap-4 md:grid-cols-2">
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-purple-300">Numeral.js</h5>
              <p class="mt-2 text-xs text-gray-400">
                A library for formatting and manipulating numbers.
              </p>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">import numeral from 'numeral'

numeral(1000).format('0,0') // '1,000'
numeral(1000).format('$0,0.00') // '$1,000.00'
numeral(0.5).format('0%') // '50%'</pre>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-purple-300">Currency.js</h5>
              <p class="mt-2 text-xs text-gray-400">
                A lightweight library for currency operations without floating point issues.
              </p>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">import currency from 'currency.js'

currency(123.5).add(0.23).format() // '$123.73'
currency(1.23).multiply(2).format() // '$2.46'
currency(10.00).subtract(5.00).format() // '$5.00'</pre>
            </div>
          </div>
        </div>
        
        <!-- UI Enhancement -->
        <div class="rounded-lg border border-gray-700 bg-gray-900 p-4">
          <div class="mb-3 flex items-center justify-between">
            <h4 class="text-sm font-medium text-white">UI Enhancement</h4>
            <div class="flex gap-2">
              <span class="rounded-full bg-purple-500/20 px-3 py-1 text-xs text-purple-300">
                Animation
              </span>
              <span class="rounded-full bg-purple-500/20 px-3 py-1 text-xs text-purple-300">
                Charts
              </span>
            </div>
          </div>
          
          <div class="grid gap-4 md:grid-cols-2">
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-purple-300">GSAP (GreenSock)</h5>
              <p class="mt-2 text-xs text-gray-400">
                Professional-grade animation library for the web.
              </p>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">import { gsap } from 'gsap'

gsap.to('.box', {
  duration: 1,
  x: 100,
  y: 50,
  rotation: 360,
  ease: 'power2.inOut'
})</pre>
            </div>
            
            <div class="rounded-lg border border-gray-700 bg-gray-800 p-3">
              <h5 class="text-xs font-medium text-purple-300">Chart.js</h5>
              <p class="mt-2 text-xs text-gray-400">
                Simple yet flexible JavaScript charting library.
              </p>
              <pre class="mt-2 overflow-x-auto rounded bg-gray-900 p-2 text-xs text-gray-300">import Chart from 'chart.js/auto'

new Chart(ctx, {
  type: 'line',
  data: {
    labels: ['Jan', 'Feb', 'Mar'],
    datasets: [{
      label: 'Sales',
      data: [30, 45, 60]
    }]
  }
})</pre>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

// Section navigation
const sections = [
  { id: 'lodash', name: 'Lodash' },
  { id: 'date-libraries', name: 'Date Libraries' },
  { id: 'other-libraries', name: 'Other Libraries' }
];
const activeSection = ref('lodash');
</script> 